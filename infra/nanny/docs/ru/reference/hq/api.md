# API

##  Intro {#intro}
В данном документе описывается RPC интерфейс сервиса HQ. На данный момент сервис предоставляет API для манипулирования описанием инстансов.

##  Протокол {#protocol}
* Все структуры данных описаны в protobuf (версии 3).
* Запросы осуществляются с помощью HTTP. Метод POST.
* Вызываемый сервис и метод (в терминах protobuf) передаёт в URL.
* Сами запросы и ответы передаются в теле.
* Поддерживаются заголовки `Content-Type:` и `Accept:`.
Можно указать либо `application/x-protobuf`, либо `application/json`.

##  Доступ {#access}
Т.к. в каждой гео локации своя независимая инсталляция, то для доступа необходимо использовать разные URL:

* MSK - `hq.msk-swat.yandex-team.ru/rpc/instances/`
* SAS - `hq.sas-swat.yandex-team.ru/rpc/instances/`
* MAN - `hq.man-swat.yandex-team.ru/rpc/instances/`
* VLA - `hq.vla-swat.yandex-team.ru/rpc/instances/`

##  Python Client {#python-client}
* Для использование необходимо установить 2 пакета (с `pypi.yandex-team.ru`):
    * `nanny_rpc_client` - реализация RPC.
    * `clusterpb` - интерфейсы для удалённых вызовов и protobuf определения объектов.

Пример команд для сборки virtualenv с необходимыми пакетами

```bash
virtualenv env
. env/bin/activate
pip install clusterpb nanny_rpc_client -i https://pypi.yandex-team.ru/simple/
```


###  Пример использования {#python-client-example}

```python
"""
В этом примере мы получим список всех известных инстансов сервиса в конкретном кластере.
"""
from nanny_rpc_client import RequestsRpcClient
from clusterpb import hq_stub  # Интерфейс удалённого RPC сервера
from clusterpb import hq_pb2  # Определения запросов и ответов сервера

# Создаём реализацию клиента, указывая URL и прочие настройки
client = RequestsRpcClient('http://hq.msk-swat.yandex-team.ru/rpc/instances/', request_timeout=10)
# Инициализируем клиент для Instance Service'а HQ
hq_client = hq_stub.InstanceServiceStub(client)
# Создаём объект запроса
find_req = hq_pb2.FindInstancesRequest()
# Указываем интересующий нас сервис
find_req.filter.service_id = 'production_nanny'
# Выполняем запрос
resp = hq_client.find_instances(find_req)
# Печатаем результат
for i in resp.instance:
    print i
```

###  Получение списка инстансов во всех кластерах {#python-client-list-all-example}

Пример на python получения полного списка инстансов сервиса

```python
"""
В этом примере мы:
  * используем federated сервис для получения всех кластеров HQ
  * затем у каждого запросим инстансы интересующего нас сервиса
"""
from nanny_rpc_client import RequestsRpcClient
# Определения запросов и ответов сервера
from clusterpb import federated_stub, federated_pb2
from clusterpb import hq_pb2, hq_stub

client = RequestsRpcClient('http://federated.yandex-team.ru/rpc/federated/', request_timeout=10)
# Инициализируем клиент для Federated Service'а
f_client = federated_stub.FederatedClusterServiceStub(client)
# Создаём объект запроса, без параметров
find_req = federated_pb2.FindClustersRequest()
# Выполняем запрос и сохраняем список кластеров
clusters = f_client.find_clusters(find_req).value
instances = []  # Здесь будем хранить список инстансов сервиса
# Создаём объект запроса (он будет один для всех кластеров)
find_req = hq_pb2.FindInstancesRequest()
# Указываем интересующий нас сервис
find_req.filter.service_id = 'production_nanny'
# Выполняем поиск инстансов в каждом кластере
for c in clusters:
    # Создаём клиент для конкретного кластера
    client = RequestsRpcClient(c.spec.endpoint.url + 'rpc/instances/', request_timeout=10)
    hq_client = hq_stub.InstanceServiceStub(client)
    resp = hq_client.find_instances(find_req)
    instances.extend(resp.instance)

for i in instances:
    print i
```


##  Примеры REST like {#rest-examples}

Т.к. API использует протокол HTTP (как описано [в документации](../rpc/design-and-feature.md), то несложно собрать примеры использования API без клиентских библиотек.

###  Получение списка инстансов во всех кластерах {#rest-list-all-example}
В этом примере мы:

* используем federated сервис для получения всех кластеров HQ
* затем у каждого запросим инстансы интересующего нас сервиса
Приступим:
* `curl -X POST --data '{}' http://federated.yandex-team.ru/rpc/federated/FindClusters/`
запрашиваем в federated сервисе список всех кластеров (если мы не знаем, где расположен сервис)

Ппример ответа

```json
$ curl -X POST --data '{}' http://federated.yandex-team.ru/rpc/federated/FindClusters/ | python -m json.tool
{
    "value": [
        {
            "meta": {
                "generation": "0",
                "name": "man_prod",
                "uuid": "",
                "version": "7"
            },
            "spec": {
                "desc": "MAN prod",
                "endpoint": {
                    "url": "http://hq.man-swat.yandex-team.ru/"
                }
            }
        },
        {
            "meta": {
                "generation": "0",
                "name": "msk_prod",
                "uuid": "",
                "version": "7"
            },
            "spec": {
                "desc": "MSK prod",
                "endpoint": {
                    "url": "http://hq.msk-swat.yandex-team.ru/"
                }
            }
        },
        {
            "meta": {
                "generation": "0",
                "name": "sas_prod",
                "uuid": "",
                "version": "7"
            },
            "spec": {
                "desc": "SAS prod",
                "endpoint": {
                    "url": "http://hq.sas-swat.yandex-team.ru/"
                }
            }
        },
        {
            "meta": {
                "generation": "0",
                "name": "vla_prod",
                "uuid": "",
                "version": "7"
            },
            "spec": {
                "desc": "VLA prod",
                "endpoint": {
                    "url": "http://hq.vla-swat.yandex-team.ru/"
                }
            }
        }
    ]
}
```

* Запрашиваем список инстансов нашего сервиса в каждом кластере

```
curl -X POST https://hq.vla-swat.yandex-team.ru/rpc/instances/FindInstances/ -d '{"filter":{"serviceId": "prestable_alemate_master"}}' | python -m json.tool
```

### Получение числа инстансов сервиса {#rest-list-stats-example}

Запросим число инстансов интересующего нас сервиса (если мы не знаем, в каком именно кластере он находится, воспользуемся federated, [как в примере выше](#rest-list-all-example)). Для этого используем метод `GetRevisionStats`, его подробное описание доступно в [porto-файле](#service-definition).

```
$ curl -X POST https://hq.sas-swat.yandex-team.ru/rpc/instances/GetRevisionStats/ -d '{"filter":{"serviceId":"rthub-pages"}}' -H 'Content-Type: application/json' | python -m json.tool
```

Ответ

```json
{
    "stats": [
        {
            "installedCount": 742,
            "readyCount": 0,
            "revision": "rthub-pages-1516631970985",
            "totalCount": 760
        },
        {
            "installedCount": 742,
            "readyCount": 0,
            "revision": "rthub-pages-1516702749306",
            "totalCount": 760
        },
        {
            "installedCount": 742,
            "readyCount": 0,
            "revision": "rthub-pages-1516737925856",
            "totalCount": 760
        },
        {
            "installedCount": 742,
            "readyCount": 742,
            "revision": "rthub-pages-1516742736789",
            "totalCount": 760
        }
    ]
}
```


####  Описание сервиса {#service-definition}

Самое актуальное описание всегда доступно в [исходном коде](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/hq/proto/hq.proto).

```
service InstanceService {
    rpc GetInstance (GetInstanceRequest) returns (GetInstanceResponse);
    rpc FindInstances (FindInstancesRequest) returns (FindInstancesResponse);
    rpc UpdateInstance (UpdateInstanceRequest) returns (UpdateInstanceResponse);
    rpc CreateInstance (CreateInstanceRequest) returns (CreateInstanceResponse);
    rpc ReportInstanceRevStatus (ReportInstanceRevStatusRequest) returns (ReportInstanceRevStatusResponse);
    rpc GetInstanceRev (GetInstanceRevRequest) returns (GetInstanceRevResponse);
    rpc AddInstanceRev (AddInstanceRevRequest) returns (AddInstanceRevResponse);
    rpc DeleteInstance (DeleteInstanceRequest) returns (DeleteInstanceResponse);
    rpc GetInstanceStats (GetInstanceStatsRequest) returns (GetInstanceStatsResponse);
    rpc GetRevisionStats (GetRevisionStatsRequest) returns (GetRevisionStatsResponse);
    rpc DeleteServiceRev (DeleteServiceRevRequest) returns (DeleteServiceRevResponse);
    rpc ListAttributeValues (ListAttributeValuesRequest) returns (ListAttributeValuesResponse);
}
```
