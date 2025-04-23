# Crowdtest для асессоров в Директе

## Наши crowdtest балансеры
  
- l7 балансер <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/show/>
- l3 балансер <https://l3.tt.yandex-team.ru/service/12550>
  
dns:  
```
crowdtest.direct.yandex.ru.   600   IN   A	 213.180.193.41
crowdtest.direct.yandex.ru.   600   IN   AAAA   2a02:6b8::3bf
  
*.crowdtest.direct.yandex.ru. 600   IN   CNAME  crowdtest.direct.yandex.ru
```

## Чек-лист поднятия crowdtest стенда
1. Создать l7 балансер в awacs в своем проекте (кнопка _Create namespace with L7_)
2. Запросить сертификат на странице Сертификатов (ссылка на страничку _Show Certificates_, кнопка _Order Cerificate_). Автоматически создастся тикет на СИБ, ждем его аппрува
3. Создать l3 балансер на странице L3 балансеров (ссылка на страничку _Show L3 Balancers_, кнопка _Create New L3 Balancer_)
4. Сделать туннели L3-L7 для всех балансеров через _reallocate pods -> advanced settings -> virtual service id -> crowdtest.{ваш_сервис}.yandex.ru_.
5. Сделать DNS записи для хоста `crowdtest.{ваш_сервис}.yandex.ru` (IP адреса берем из конфига L3 балансера)
6. Сделать CNAME `*.crowdtest.{ваш_сервис}.yandex.{ru,com}` в `crowdtest.{ваш_сервис}.yandex.ru`
7. Создать бекенд, апстрим и домен (по описанию ниже) 
8. Для каждого L7 прописать в YAML spec:  
```yaml 
https:
    enable_tlsv1_3: true
 include_domains: {}
  webauth:
    mode: EXTERNAL
    action: AUTHENTICATE_USING_IDM
```
9. Создать тикет в BALANCERSUPPORT на подключение webauth
10. Запросить роль в IDM для своей команды и на группу тестирования асессорами: [доступ в idm](https://idm.yandex-team.ru/system/webauth-awacs/roles#f-status=all,f-role=webauth-awacs,sort-by=-updated,f-ownership=group,role=33925770)
11. Заказать дырки через puncher наружу (от any) до вашего балансера, ждать аппрува от СИБ
12. Проверить, что ваши балансеры живут в вашем макросе, чтобы был доступ. Перенести в свой макрос, если это не так
13. Открыть свой стенд, убедиться, что работает 2фа и стенд открывается

## Добавление нового сервиса 
_Скопировано со странички <https://wiki.yandex-team.ru/jandexmetrika/frontend/crowdtest>_

Чтобы добавить новый сервис, в awacs-балансере нужно добавить три сущности в таком порядке:  
- бекенд - содержит информацию о получателе трафика
- апстрим - содержит в себе часть конфига балансера, обычно логически изолированную. Через апстрим проходит трафик, прежде чем пойти в бекенд
- домен - содержит набор FQDN'ов (доменных имён), сертификат для HTTPS и набор апстримов, которые будут обслуживать запросы, пришедшие на FQDN'ы домена

### Добавляем бекенд
В awacs есть несколько типов бекендов. Это может быть nanny-сервис или снапшот, gencfg-группа или yp-endpointset. Мы же будем использовать Manual, то есть вручную зададим хост и порт  
  
Переходим на вкладку [Show backends](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/backends/list/) и жмём кнопку [Create backend](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/backends/create/).  
- **Id** - заполняем адресом тестовой среды, например test.direct.yandex.ru
- **Type** - Manual
- Жмём Create
  
Сразу же жмём **Create or edit current endpoint set** и заполняем форму  
- **Host** - test.direct.yandex.ru
- **Port** - 443
- **Weight** - 1
- **IPv6 address** - нужно выяснить с помощью команды host  
```bash
> host test.direct.yandex.ru

test.direct.yandex.ru has IPv6 address 2a02:6b8:0:3400:0:a9:0:1b
```

{% cut "скрин добавленного шаблона" %}

![alt text](https://jing.yandex-team.ru/files/rifler/2021-01-18_22-53-22.png)  

{% endcut %}
  
Жмём Save и ждём, пока на странице списка бекендов всё позеленеет. Это значит что бекенд добавлен  
  
### Добавляем апстрим
Переходим на вкладку [Show upstreams](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/upstreams/list/) и жмём кнопку [Create upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.metrika.yandex.ru/upstreams/create/) и заполняем: direct  
- **Id** - точки запрещены, поэтому можно назвать именем сервиса, например **direct** или **release**  
- **Mode** - Easy
- **YAML spec** - лучше скопировать из уже существующего апстрима, заменив все идентификаторы на свои

   {% cut "пример" %}  

    ```yaml
    l7_upstream_macro:
      version: 0.0.1
      id: direct
      matcher:
        host_re: '.*'
      flat_scheme:
        balancer:
          use_https_to_endpoints: {}
          attempts: 2
          fast_attempts: 2
          max_reattempts_share: 0.15
          max_pessimized_endpoints_share: 0.2
          retry_http_responses:
            codes: [5xx]
          backend_timeout: 3600s
          connect_timeout: 125ms
        backend_ids: [test-direct.yandex.ru]
        on_error:
          static:
            status: 504
            content: "Service unavailable"
    ```
    
    {% endcut %}
  
Жмём Save и ждём, пока на странице списка апстримов всё позеленеет.  
  
### Добавляем домен
Жмём на кнопку [Create domain](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/domains/create/) и заполняем  
  
- **Id** - заполняем адресом нового краудтест-домена, например release.crowdtest.direct.yandex.ru
- **Domain type** - Common
- **Primary FQDNS** - домены, разделенные через запятую. Например `release.crowdtest.direct.yandex.ru,release.crowdtest.direct.yandex.com`
- **Upstreams** - Choose upstreams to include, из выпадающего списка выбираем недавно созданный апстрим
- **Certificates** - Use a single certificate → Use existing certificate и из выпадающего списка выбираем crowdtest.direct.yandex.ru
