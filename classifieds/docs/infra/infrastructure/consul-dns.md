{% note warning %}

Консул-днс можно использовать для походов из одного сервиса в другой, но предпочтительным является использование балансеров, так как балансировщики "из коробки" дают графики/трейсы/балансировку раунд-робином и правильный увод трафика с сервиса во время учений с закрытием ДЦ.

{% endnote %}

###  Архитектура

1. На всех наших серверах установлен кеширующий и рекурсивный  DNS сервер [unbound](https://nlnetlabs.nl/projects/unbound/about/)  
2. В каждом датацентре, в тестинге и проде, есть кластера консул-серверов, на всех остальных машинках установлены консул-агенты.
3. `unbound` на машинках с консул-агентами пересылают запросы зоны `.consul` в `unbound` на консул-серверах в своём ДЦ 
4. `unbound` на машинках с консул-серверами пересылает запросы зоны `.consul` в свой консул-сервер.  
5. Все unbound-ы кешируют ответы про зону `.consul` на 1 секунду

### Консул днс

Если инстансы сервиса зарегистрированы в консуле и прошли проверки живости, то их IP адреса можно получить отправив днс запрос в консул сервер, а так как `unbound` на каждом сервере уже настроен на работу с консулом, то для днс запроса указывать отдельный резолвер не нужно, то есть с зоной `.consul` можно работать так же как и со всеми остальными зонами.

Получить IP адреса инстансов сервиса можно разными способами.  
Шаблоны запросов:
| Запрос | Какую информацию вернёт |
|--------|-------------------------|
| `<service_name>.service.consul` | IP адреса всех инстансов `<service_name>` в текущем датацентре |
| `<service_name>.service.<dc>.consul` | IP адреса всех инстансов `<service_name>` в датацентре <dc> |
| `<service_name>.query.consul` | IP адреса всех инстансов `<service_name>` в текущем датацентре , если таких нет, то IP адреса всех инстансов `<service_name>` из соседнего датацентра |

Так же, по консул днс, можно получить адреса инстансов сервиса с определенным тегом, добавив к запросу тег, например: `<tag>.<service_name>.service.<dc>.consul` или `<tag>.<service_name>.query.consul`.  

Примеры запросов:  
<details>  
<summary>Получение всех IP адреса сервиса nomad-ui-http в датацентре SAS</summary>  

 ```  
host nomad-ui-http.service.sas.consul
nomad-ui-http.service.sas.consul has IPv6 address 2a02:6b8:c14:408e:8000:4098:f:935
nomad-ui-http.service.sas.consul has IPv6 address 2a02:6b8:c02:900:1:20:f14:c3
nomad-ui-http.service.sas.consul has IPv6 address 2a02:6b8:c14:4091:8000:4098:f:ce
nomad-ui-http.service.sas.consul has IPv6 address 2a02:6b8:c14:40a1:8000:4098:f:147
 ```
</details>

<details>  
<summary>Получение всех IP адресов сервиса nomad-ui-http в текущем датацентре, либо из соседнего датацентра, если в текущем нет живых инстансов</summary>  

 ```  
host nomad-ui-http.query.consul
nomad-ui-http.query.consul has IPv6 address 2a02:6b8:c1f:108f:0:1459:f:3143
nomad-ui-http.query.consul has IPv6 address 2a02:6b8:c0e:500:1:d:f43:5132
nomad-ui-http.query.consul has IPv6 address 2a02:6b8:c0e:500:1:d:f47:57cb
nomad-ui-http.query.consul has IPv6 address 2a02:6b8:c1f:1091:0:1459:f:1fdc
 ```
</details>

### Consul днс с личных ноутбуков.

По дефолту резолв зоны `.consul` настроен только на боевых/тестовых/dev серверах и не работает на личных ноутбуках.

Для резолва зоны `.consul` с личных ноутбуков можно использовать поднятый для этого балансировщик: "consul-dns-test-int.noc-slb.vertis.yandex.net". Доступ к нему уже есть у всех разработчиков Вертикалей. Он принимает запросы на стандартный 53 порт (TCP/UDP).  
Для получения IP адресов можно использовать как любые популярные утилиты:  
<details>  
<summary>dig</summary>
Формат команды: 

``
dig @consul-dns-test-int.noc-slb.vertis.yandex.net <консул-днс имя> AAAA
``  
Пример:

 ```
dig @consul-dns-test-int.noc-slb.vertis.yandex.net broker-api-grpc-api.query.consul AAAA

; <<>> DiG 9.16.1-Ubuntu <<>> @consul-dns-test-int.noc-slb.vertis.yandex.net broker-api-grpc-api.query.consul AAAA
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12772
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;broker-api-grpc-api.query.consul. IN	AAAA

;; ANSWER SECTION:
broker-api-grpc-api.query.consul. 1 IN	AAAA	2a02:6b8:c07:89f:0:1459:f:4d09
broker-api-grpc-api.query.consul. 1 IN	AAAA	2a02:6b8:c02:900:1:d:f19:ccb
broker-api-grpc-api.query.consul. 1 IN	AAAA	2a02:6b8:c23:2e22:0:1459:f:aa32
broker-api-grpc-api.query.consul. 1 IN	AAAA	2a02:6b8:c08:e428:0:1459:f:591f

;; Query time: 3 msec
;; SERVER: 2a02:6b8:0:3400:0:4f1:0:52#53(2a02:6b8:0:3400:0:4f1:0:52)
;; WHEN: Tue Jul 05 18:45:02 MSK 2022
;; MSG SIZE  rcvd: 173
 ```
</details>
<details>  
<summary>host</summary>
Формат команды: 

``
host <консул-днс имя> consul-dns-test-int.noc-slb.vertis.yandex.net
``  
Пример:

 ```
host broker-api-grpc-api.query.consul consul-dns-test-int.noc-slb.vertis.yandex.net
Using domain server:
Name: consul-dns-test-int.noc-slb.vertis.yandex.net
Address: 2a02:6b8:0:3400:0:4f1:0:52#53
Aliases:

broker-api-grpc-api.query.consul has IPv6 address 2a02:6b8:c23:2e22:0:1459:f:aa32
broker-api-grpc-api.query.consul has IPv6 address 2a02:6b8:c07:89f:0:1459:f:4d09
broker-api-grpc-api.query.consul has IPv6 address 2a02:6b8:c02:900:1:d:f19:ccb
broker-api-grpc-api.query.consul has IPv6 address 2a02:6b8:c08:e428:0:1459:f:591f
 ```
 </details>
 <details>  
<summary>nslookup</summary>
Формат команды: 

``
nslookup <консул-днс имя> consul-dns-test-int.noc-slb.vertis.yandex.net
``  
Пример:

 ```
 nslookup broker-api-grpc-api.query.consul consul-dns-test-int.noc-slb.vertis.yandex.net
Server:		consul-dns-test-int.noc-slb.vertis.yandex.net
Address:	2a02:6b8:0:3400:0:4f1:0:52#53

Non-authoritative answer:
Name:	broker-api-grpc-api.query.consul
Address: 2a02:6b8:c08:e428:0:1459:f:591f
Name:	broker-api-grpc-api.query.consul
Address: 2a02:6b8:c07:89f:0:1459:f:4d09
Name:	broker-api-grpc-api.query.consul
Address: 2a02:6b8:c23:2e22:0:1459:f:aa32
Name:	broker-api-grpc-api.query.consul
Address: 2a02:6b8:c02:900:1:d:f19:ccb
```
</details>
так и любые другие.    

#### Настройка постоянного резолвинга зоны .consul  
Есть несколько способов настроить постоянный резолвинг зоны `.consul` с локального ноутбука, все они  имеют свои плюсы и минусы. 
1. С помощью системного резолвера macOS (! замечено, что не все утилиты работают с данным способом, то есть, например, `ping6` работать будет, а утилита `host` - нет.)
   1. Создаём каталог `/etc/resolver/`  
   2. Кладём в него файл `consul` с содержимым:  
        ```
        nameserver 2a02:6b8:0:3400:0:4f1:0:52
        port 53
        ```  
   3. Проверяем, что зона резолвится: `ping6 consul.query.consul` 

2. С помощью утилиты [dnsmasq](https://dnsmasq.org) (! способ не проверялся)
   1. Устанавливаем `dnsmasq` через brew/apt либо любым другим доступным способом.  
   2. Создаём файл `/etc/dnsmasq.d/10-consul` с содержимым:
       ```
       # Enable forward lookup of the 'consul' domain:
       server=/consul/2a02:6b8:0:3400:0:4f1:0:52#8600
       ````
3. Любым другим способом.  
       Гайд от разработчиков консула: [https://learn.hashicorp.com/tutorials/consul/dns-forwarding](https://learn.hashicorp.com/tutorials/consul/dns-forwarding).  
