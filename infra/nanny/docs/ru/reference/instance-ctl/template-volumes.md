# Шаблонизация файлов с помощью InstanceCtl

## Что это? {#intro}

Механизм шаблонизации клиентских файлов во время деплоя сервиса. Необходимо использовать InstanceCtl версии ≥ **1.4**.

Тикет с обсуждением этой функциональности: [SWAT-3174](https://st.yandex-team.ru/SWAT-3174).

## Схема работы {#how-does-it-work}

1. В спецификации инстансов сервиса указываются пути к файлам шаблонов, файлы приносятся в ресурсах сервиса.
1. На конечном хосте InstanceCtl перед каждым запуском инстанса:
    * Шаблонизирует все указанные в спецификации файлы;
    * Если шаблонизация завершится с ошибкой, процесс остановится, `install_script` не будет запущен.

## Создание Template Volume {#create-template-volume}

Добавить `instance data volume` в `Instance Spec`, выбрать тип `TEMPLATE`, добавить нужное количество шаблонов, указать путь к файлу шаблона и путь, куда положить готовый файл.

![img](https://jing.yandex-team.ru/files/sshipkov/templatevolumes.1c5c234.png)

Результаты шаблонизации будут находиться по адресу `<instance_folder>/<volume_name>/<destination_file_path>`.

### Замечания {#path-notes}

* файл `Source file path` и все включаемые с помощью `include` в шаблон файлы должны находиться в директории инстанса или во вложенных в нее директориях. Например, эти файлы можно создать в Static files сервиса.
* путь `Destination file path` не должен конфликтовать с принесенными в сервисе ресурсами и другими `Destination file path` своего `volume`

## Контекст шаблонов {#template-context}

В контекст шаблонизации входит:

1. переменные из [iss-окружения](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/instancectl/#iss-loop-conf-render-params);
1. словарь ортогональных тегов `orthogonal_tags` [подробнее](https://wiki.yandex-team.ru/jandekspoisk/sepe/instancectl/#ortho-tags)
1. функция `get_hq_instances(service_id)` – получает все инстансы сервиса `service_id` из всех кластеров HQ, возвращает список объектов типа `Instance`, схема которых описана в `protobuf`: [описание формата](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/instancectl/src/protobuf/clusterpb/types.proto?blame=true&rev=5462212#L421). Не работает при недоступности хотя бы одного кластера HQ даже если в нём нет инстансов интересующего сервиса.
1. функция `get_hq_instances_current_cluster(service_id)` – получает все инстансы сервиса `service_id` **только из того же кластера** HQ, в котором находится инстанс. Возвращает значение того же типа, что и функция `get_hq_instances`. (требуется Instancectl ≥ **1.158**)
1. функция `get_hq_instances(service_id, ["MAN", "VLA", ...])` – получает все инстансы сервиса `service_id` **из заданного списка кластеров** HQ. Возвращает значение того же типа, что и функция `get_hq_instances`. (требуется Instancectl ≥ **1.158**)
1. переменная `CURRENT_REV` – текущая ревизия сервиса в HQ, совпадает с id конфигурации сервиса (требуется Instancectl ≥ **1.47**)
1. функции `resolve_ipv6_addr(host)` и `resolve_ipv4_addr(host)` – возвращают список различных ip-адресов для указанного имени, v6 и v4 соответственно (требуется Instancectl ≥ **1.52**)
1. функция `get_sd_endpoints(endpoint_set_id, cluster_names)` — получает `endpoint`'ы из всех кластеров указанных в `cluster_names` (если не передан `cluster_names`, список кластеров становится: `["SAS", "MAN", "VLA", "IVA", "MYT"]`), возвращает объекты типа [TEndpoint](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto?rev=r7460597#L7), если в результате не будет найдено ни одного `endpoint`'а то шаблонизатор упадет с ошибкой. (требуется Instancectl ≥ **2.54**)
2. функция `get_sd_endpoints_current_cluster(endpoint_set_id)` — аналогично функции `get_sd_endpoints`, только для того кластера в котором находится инстанс, для инстансов которые аллоцированы в `["SAS-TEST", "MAN-PRE", "XDC"]` будут возвращаться `endpoint`'ы из кластера в котором реально находится инстанс ([https://st.yandex-team.ru/SWAT-7578](https://st.yandex-team.ru/SWAT-7578)) (требуется Instancectl ≥ **2.54**)
3. функция `get_sd_pods(service_id, cluster_names)` — получает `pod`'ы из всех кластеров указанных в `cluster_names`(если не передан `cluster_names`, список кластеров становится: `["SAS", "MAN", "VLA", "IVA", "MYT"]`), возвращает объекты типа [TPod](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto?rev=r7460597#L51), если в результате не будет найдено ни одного `endpoint`'а то шаблонизатор упадет с ошибкой. (требуется Instancectl ≥ **2.54**)
4. функция `get_sd_pods_current_cluster(service_id)` — аналогично фукнции `get_sd_pods`, только для того кластера в котором находится инстанс, для инстансов которые аллоцированы в `["SAS-TEST", "MAN-PRE", "XDC"]` будут возвращаться `pod`'ы из кластера в котором реально находится инстанс ([https://st.yandex-team.ru/SWAT-7578](https://st.yandex-team.ru/SWAT-7578)) (требуется Instancectl ≥ **2.54**)

## Фильтры {#filters}

Доступны следующие jinja filters (версия Instancectl ≥ **1.7**):

Для результата функции `get_hq_instances`:

* `last_revision` – получить инстансы самой последней ревизии;
* `alive` – получить инстансы, которые сейчас живы (хотя бы одна ревизия данного инстанса активна). Для использования этой функциональности необходимо, чтобы сервис, живые инстансы которого мы хотим получить, также использовал свежий InstanceCtl;
* `alive_or_last_revision` – получить инстансы, которые сейчас живы, если таких нет, получить инстансы с последней ревизией.
* `revision_filter(revision_id)` – получить инстансы, для выбранной ревизии, в `instance.spec.revision` будут только объекты Revision выбранной ревизии (требуется Instancectl ≥ **1.47**)

Для результата функции `get_sd_endpoints`:

* `ready_endpoints` – получить `endpoint`'ы у которых `endpoint.ready == True` (требуется Instancectl ≥ **2.53**)

## Доставка шаблонов в виде архива {#archive}

Шаблоны можно доставлять в контейнеры в виде архива. Для этого достаточно принести их в виде слоя файловой системы. Достаточно сложить шаблоны в директорию `templates` заархивировать вместе с директорией в `templates.tar.gz`, и вписать получившийся архив в список слоёв в `Instance Spec`. Шаблоны будут доступны в директории `/templates` (прямо от корня файловой системы) уже в распакованном виде.

## Локальное тестирование шаблонов {#local-testing}

Собираем утилиту

```
cd ./arcadia;
./ya make --checkout infra/nanny/nanny_jinja_template
cd infra/nanny/nanny_jinja_template
```

Пишем шаблон, например с таким содержанием

template_mongo.conf:

```yaml
storage:
  dbPath: {{ HOME }}/mongodb
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /logs/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: {{ resolve_ipv6_addr(HOSTNAME)[0] }}, 127.0.0.1
```

Запускаем (для сервисов под YP-lite)

```
./bin/njt --service rtc_planned_work -i dt16o16b014gz.man.yp-c.yandex.net  -s ./template_mongo.conf -d ./result.conf
```

Команду запуска для сервисов на gencfg можно посмотреть в [readme](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/nanny_jinja_template).

Результат

```
$ cat ./result.conf
storage:
  dbPath: /place/db/iss3/instances/80_rtc_planned_work_MeGaHaSh/mongodb
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /logs/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 2a02:6b8:c0b:3413::4405:f318:0, 127.0.0.1
```

{% note info %}

Больше примеров и readme.md есть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/nanny_jinja_template)

{% endnote %}

## Примеры {#example}

### Общий пример (использование переменных) {#general-example}

```
http_port={{ BSCONFIG_IPORT }}
redis_port={{ BSCONFIG_IPORT|int + 1 }}
location={{ orthogonal_tags['a_geo'] }}
dc={{ orthogonal_tags['a_dc'] }}
```

Результат:

```
http_port=17319
redis_port=17320
location=msk
dc=iva
```

### Функция get_hq_instances {#get-hq-instances}

```
{%- for instance in get_hq_instances("any_service") %}
{{ instance.spec.node_name }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
```
Результат:

```
sas1-1112.search.yandex.net:8082
sas1-1111.search.yandex.net:8082
```

### Функции get_sd_{endpoints|pods} {#get-sd}

{% cut "Пример кода" %}

```
# TESTING get_sd_endpoints
endpoints_all_clusters:
{%- for e in get_sd_endpoints("i-dyachkov-hq-only-status") %}
 - id: {{e.id}}
   protocol: {{e.protocol}}
   fqdn: {{e.fqdn}}
   ip6_address: {{e.ip6_address}}
   port: {{e.port}}
   ready: {{e.ready}}
{%- endfor %}
ready_endpoints:
{%- for e in get_sd_endpoints("i-dyachkov-hq-only-status") | ready_endpoints %}
 - id: {{e.id}}
   protocol: {{e.protocol}}
   fqdn: {{e.fqdn}}
   ip6_address: {{e.ip6_address}}
   port: {{e.port}}
   ready: {{e.ready}}
{%- endfor %}
endpoints_current_cluster:
{%- for e in get_sd_endpoints_current_cluster("i-dyachkov-hq-only-status") %}
 - id: {{e.id}}
   protocol: {{e.protocol}}
   fqdn: {{e.fqdn}}
   ip6_address: {{e.ip6_address}}
   port: {{e.port}}
{%- endfor %}
endpoints_man:
{%- for e in get_sd_endpoints("i-dyachkov-hq-only-status", ["MAN"]) %}
 - id: {{e.id}}
   protocol: {{e.protocol}}
   fqdn: {{e.fqdn}}
   ip6_address: {{e.ip6_address}}
   port: {{e.port}}
{%- endfor %}
# TESTING get_sd_pods
podss_all_clusters:
{%- for p in get_sd_pods("i-dyachkov-hq-only-status") %}
 - id: {{p.id}}
   node_id: {{p.node_id}}
   dns_persistent_fqdn: {{p.dns.persistent_fqdn}}
   dns_transient_fqdn: {{p.dns.transient_fqdn}}
{%- endfor %}
pods_current_cluster:
{%- for p in get_sd_pods_current_cluster("i-dyachkov-hq-only-status") %}
 - id: {{p.id}}
   node_id: {{p.node_id}}
   dns_persistent_fqdn: {{p.dns.persistent_fqdn}}
   dns_transient_fqdn: {{p.dns.transient_fqdn}}
{%- endfor %}
pods_man:
{%- for p in get_sd_pods("i-dyachkov-hq-only-status", ["MAN"]) %}
 - id: {{p.id}}
   node_id: {{p.node_id}}
   dns_persistent_fqdn: {{p.dns.persistent_fqdn}}
   dns_transient_fqdn: {{p.dns.transient_fqdn}}
{%- endfor %}
```

{% endcut %}


{% cut "Результат" %}

```
# TESTING get_sd_endpoints
endpoints_all_clusters:
 - id: aztdr4hzzlqr3ur6
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c1b:3789:0:696:6b9e:0
   port: 80
   ready: True
 - id: fp9e7jxoclauupke
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c14:4300:0:696:458d:0
   port: 80
   ready: True
 - id: 6tq38u491q48vfb8
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
   ip6_address: 2a02:6b8:c26:a33:0:696:be56:0
   port: 80
   ready: True
 - id: xphzgvx963xsz3ez
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.vla.yp-c.yandex.net
   ip6_address: 2a02:6b8:c0f:9e:0:696:2255:0
   port: 80
   ready: True
 - id: 715rbfjt0e4j53fy
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.iva.yp-c.yandex.net
   ip6_address: 2a02:6b8:c0c:848a:0:696:e3be:0
   port: 80
   ready: True
 - id: wrpzeusoyg2oq1gu
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.myt.yp-c.yandex.net
   ip6_address: 2a02:6b8:c12:3fad:0:696:acff:0
   port: 80
   ready: True
ready_endpoints:
 - id: aztdr4hzzlqr3ur6
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c1b:3789:0:696:6b9e:0
   port: 80
   ready: True
 - id: fp9e7jxoclauupke
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c14:4300:0:696:458d:0
   port: 80
   ready: True
 - id: 6tq38u491q48vfb8
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
   ip6_address: 2a02:6b8:c26:a33:0:696:be56:0
   port: 80
   ready: True
 - id: xphzgvx963xsz3ez
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.vla.yp-c.yandex.net
   ip6_address: 2a02:6b8:c0f:9e:0:696:2255:0
   port: 80
   ready: True
 - id: 715rbfjt0e4j53fy
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.iva.yp-c.yandex.net
   ip6_address: 2a02:6b8:c0c:848a:0:696:e3be:0
   port: 80
   ready: True
 - id: wrpzeusoyg2oq1gu
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.myt.yp-c.yandex.net
   ip6_address: 2a02:6b8:c12:3fad:0:696:acff:0
   port: 80
   ready: True
endpoints_current_cluster:
 - id: aztdr4hzzlqr3ur6
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c1b:3789:0:696:6b9e:0
   port: 80
 - id: fp9e7jxoclauupke
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
   ip6_address: 2a02:6b8:c14:4300:0:696:458d:0
   port: 80
endpoints_man:
 - id: 6tq38u491q48vfb8
   protocol: TCP
   fqdn: i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
   ip6_address: 2a02:6b8:c26:a33:0:696:be56:0
   port: 80
# TESTING get_sd_pods
podss_all_clusters:
 - id: i-dyachkov-hq-only-status-1
   node_id: sas2-5944.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
   dns_transient_fqdn: sas2-5944-1.i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-2
   node_id: sas5-6755.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
   dns_transient_fqdn: sas5-6755-1.i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-1
   node_id: man0-3236.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
   dns_transient_fqdn: man0-3236-1.i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-1
   node_id: vla0-3896.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.vla.yp-c.yandex.net
   dns_transient_fqdn: vla0-3896-1.i-dyachkov-hq-only-status-1.vla.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-1
   node_id: iva0-0592.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.iva.yp-c.yandex.net
   dns_transient_fqdn: iva0-0592-1.i-dyachkov-hq-only-status-1.iva.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-1
   node_id: myt0-1660.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.myt.yp-c.yandex.net
   dns_transient_fqdn: myt0-1660-1.i-dyachkov-hq-only-status-1.myt.yp-c.yandex.net
pods_current_cluster:
 - id: i-dyachkov-hq-only-status-1
   node_id: sas2-5944.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
   dns_transient_fqdn: sas2-5944-1.i-dyachkov-hq-only-status-1.sas.yp-c.yandex.net
 - id: i-dyachkov-hq-only-status-2
   node_id: sas5-6755.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
   dns_transient_fqdn: sas5-6755-1.i-dyachkov-hq-only-status-2.sas.yp-c.yandex.net
pods_man:
 - id: i-dyachkov-hq-only-status-1
   node_id: man0-3236.search.yandex.net
   dns_persistent_fqdn: i-dyachkov-hq-only-status-1.man.yp-c.yandex.net
   dns_transient_fqdn: man0-3236-1.i-dyachkov-hq-only-status-1.man.yp-c.yandex.ne
```

{% endcut %}

### Фильтры инстансов {#instances-filter}

{% cut "Пример кода" %}

```
last_revision_filter:
{%- for instance in get_hq_instances("any_service")|last_revision %}
{{ instance.spec.node_name }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
alive_filter:
{%- for instance in get_hq_instances("any_service")|alive %}
{{ instance.spec.node_name }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
revision_filter:
{%- for instance in get_hq_instances("any_service")|revision_filter("any_service-123456789") %}
{{ instance.spec.node_name }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
self revision_filter:
{%- for instance in get_hq_instances(NANNY_SERVICE_ID)|revision_filter(CURRENT_REV) %}
{{ instance.spec.node_name }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
```

{% endcut %}

{% cut "Результат" %}

```
last_revision_filter:
sas1-1112.search.yandex.net:8082
alive_filter:
sas1-1111.search.yandex.net:8082
revision_filter:
sas1-1113.search.yandex.net:8082
self revision_filter:
iva1-0000.searhc.yandex.net:8000
```

{% endcut %}


### hostname с изоляцией по сети в сервисе {#net-isolation}

{% cut "Получить свой адрес" %}

```
{%- for instance in get_hq_instances("any_service") %}
{{ instance.spec.hostname }}:{{ instance.spec.allocation.port.0.port }}
{%- endfor %}
```

{% endcut %}

{% cut "Результат" %}

```
sas1-1111-any-service-8082.gencfg-c.yandex.net:8082
sas1-1112-any-service-8082.gencfg-c.yandex.net:8082
```

{% endcut %}

### Группировка инстансов по шардам {#group-by-shards}

На пример части конфига для Clickhouse-server'a ( пример сервиса [https://nanny.yandex-team.ru/ui/#/services/catalog/clickhouse_template/files](https://nanny.yandex-team.ru/ui/#/services/catalog/clickhouse_template/files) )

{% cut "Результат" %}

```xml
<yandex>
    <remote_servers>
    	<cluster>
            <!-- shard name clickhouse-000-0000000000 -->
            <shard>
                <replica>
                    <host>man1-1170.search.yandex.net</host>
                    <port>9000</port>
                </replica>
                <replica>
                    <host>sas1-9562.search.yandex.net</host>
                    <port>9000</port>
                </replica>
                <replica>
                    <host>vla1-0235.search.yandex.net</host>
                    <port>9000</port>
                </replica>
            </shard>
            <!-- shard name clickhouse-001-0000000000 -->
            <shard>
                <replica>
                    <host>man1-4513.search.yandex.net</host>
                    <port>9000</port>
                </replica>
                <replica>
                    <host>sas2-0199.search.yandex.net</host>
                    <port>9000</port>
                </replica>
                <replica>
                    <host>vla1-0286.search.yandex.net</host>
                    <port>9000</port>
                </replica>
            </shard>
    	</cluster>
    </remote_servers>
	<zookeeper>
            <node index="1">
            	<host>man1-1170.search.yandex.net</host>
                <port>3000</port>
            </node>
            <node index="2">
            	<host>man1-4513.search.yandex.net</host>
                <port>3000</port>
            </node>
            <node index="3">
            	<host>sas2-0199.search.yandex.net</host>
                <port>3000</port>
            </node>
            <node index="4">
            	<host>sas1-9562.search.yandex.net</host>
                <port>3000</port>
            </node>
            <node index="5">
            	<host>vla1-0235.search.yandex.net</host>
                <port>3000</port>
            </node>
            <node index="6">
            	<host>vla1-0286.search.yandex.net</host>
                <port>3000</port>
            </node>
    </zookeeper>
    <networks>
        	<host>man1-1170.search.yandex.net</host>
        	<host>man1-4513.search.yandex.net</host>
        	<host>sas2-0199.search.yandex.net</host>
        	<host>sas1-9562.search.yandex.net</host>
        	<host>vla1-0235.search.yandex.net</host>
        	<host>vla1-0286.search.yandex.net</host>
    </networks>
</yandex>
```

{% endcut %}

{% cut "Шаблон" %}

```xml
<yandex>
    <remote_servers>
    	<cluster>
       	<cluster>
            {%- for instance in get_hq_instances(NANNY_SERVICE_ID)|revision_filter(CURRENT_REV)|groupby('spec.revision.0.shard_name') %}
            <!-- shard name {{ instance.grouper }} -->
            <shard>
            {%- for inst in instance.list | sort(attribute='spec.hostname') %}
                <replica>
                	<host>{{ inst.spec.hostname }}</host>
                    <port>9000</port>
                </replica>
            {%- endfor %}
            </shard>{%- endfor %}
    	</cluster>
	</remote_servers>

	<zookeeper>
    	{%- set i_node = 1 %}
    	{%- for instance in get_hq_instances(NANNY_SERVICE_ID)|revision_filter(CURRENT_REV) | sort(attribute='spec.hostname') %}
        	<node index="{{ i_node }}">
            	<host>{{ instance.spec.hostname }}</host>
                <port>3000</port>
            </node>
            {%- set i_node = i_node + 1 %}
        {%- endfor %}
    </zookeeper>
	<networks>
    	{%- for instance in get_hq_instances(NANNY_SERVICE_ID)|revision_filter(CURRENT_REV) %}
        	<host>{{ instance.spec.hostname }}</host>
        {%- endfor %}
    </networks>
</yandex>
```

{% endcut %}


### Разрезолв FQDN (получение ip адреса из домена) {#resolve-fqdn}

{% cut "Получить свой адрес" %}

```
 Мой ip-address v6: {{ resolve_ipv6_addr(HOSTNAME)[0] }}
 Мой ip-address v4: {{ resolve_ipv4_addr(HOSTNAME)[0] }}
```

{% endcut %}

{% cut "Результат" %}

```
 Мой ip-address v6: 2a02:6b8:c0b:3961:10b:8c01::72e2
 Мой ip-address v4: 10.10.0.1
```

{% endcut %}

{% cut "Вывести список A-для домена" %}

```
 Resolv for yandex.ru
 {% for ip in resolve_ipv4_addr('yandex.ru') %}
 IP: {{ ip }}
 {% endfor %}
```

{% endcut %}

{% cut "Результат" %}

```
 Resolv for yandex.ru
 IP: 77.88.55.70
 IP: 77.88.55.80
 IP: 5.255.255.80
 IP: 5.255.255.70
```

{% endcut %}

Тоже самое можно повторить с ipv6 используя функцию **resolve_ipv6_addr**
