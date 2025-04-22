
# Endpoints resolver via YP Service Discovery
Библиотека для получения *endpoint*'ов сервиса с помощью YP Service Discovery.

Список *endpoint*'ов можно получить, зная идентификатор *endpoint_set*'а и имя YP кластера.
Список *pod*'ов можно получить, зная идентификатор *pod_set*'а и имя YP кластера.

### Важно иметь в виду
* Реплики в YP SD являются полностью независимыми, поэтому разные инстансы могут отдавать данные за разные моменты времени. Обязательно нужно учитывать **timestamp** и забирать только более новые данные.

### Resolver
* **client_name** &mdash; имя пользователя для идентификации на стороне YP Service Discovery; желательно также передать имя хоста, с которого совершается запрос; на запросы с пустым **client_name** YP SD отвечает пустым ответом
* **grpc_address** &mdash; gRPC адрес YP Service Discovery; это **sd.yandex.net:8081**, также есть полокационные балансеры **{sas,man,vla,msk}.sd.yandex.net:8081**.
* **timeout** &mdash; таймаут на запрос; если достигается, бросается исключение.

```py
import socket
from infra.yp_service_discovery.python.resolver.resolver import Resolver
...
resolver = Resolver(client_name='test:{}'.format(socket.gethostname()), timeout=5)
```

### Получение списка *endpoint*'ов

#### Запрос
Можно сделать, передав proto message `TReqResolveEndpoints`, описанный в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto), в метод `resolve_endpoints`:
```py
from infra.yp_service_discovery.api import api_pb2
...
request = api_pb2.TReqResolveEndpoints()
request.cluster_name = 'sas'
request.endpoint_set_id = 'chaos-service-slave'
request.client_name = 'chaos-service-resolver:{}'.format(socket.gethostname())
request.label_selectors.append('path/to/label')
request.ruid = 'resolve-chaos-service-in-sas'

result = resolver.resolve_endpoints(request)
```

`TRspResolveEndpoints`:
* **cluster_name** (required) &mdash; имя YP кластера
* **endpoint_set_id** (required) &mdash; идентификатор *endpoint_set*'а
* **client_name** &mdash; имя пользователя для идентификации на стороне YP Service Discovery; перезаписывает значение **client_name**, установленное при инициализации `Resolver`
* **label_selectors** &mdash; список путей в `/labels`, по которым нужно получить значения
* **watch_token** &mdash; *DEPRECATED*
* **ruid** &mdash; произвольная строка для идентификации запроса, значение будет установлено в поле **ruid** в ответе

#### Ответ
Возвращается в виде proto-сообщения `TRspResolveEndpoints`, определенного в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto),
* **timestamp** &mdash; YP timestamp версии данных
* **endpoint_set** &mdash; `TEndpointSet`
* **resolve_status** &mdash; статус `NOT_EXISTS` (*endpoint_set*'а не существует), `NOT_CHANGED` (*DEPRECATED*), `OK`
* **watch_token** &mdash; *DEPRECATED*
* **host** &mdash; имя хоста YP Service Discovery, с которого пришел ответ
* **ruid** &mdash; равен **ruid** из запроса или рандомному значению, если **ruid** не был передан

`TEndpointSet`:
* **endpoint_set_id** &mdash; идентификатор *endpoint_set*'а
* **endpoints** &mdash; список *endpoint*'ов (`TEndpoint`)
    * **id** &mdash; идентификатор *endpoint*'а
    * **protocol** &mdash; протокол подключения (TCP или UDP)
    * **fqdn** &mdash; переменный fqdn
    * **ip4_address** &mdash; IPv4 адрес
    * **ip6_address** &mdash; IPv6 адрес
    * **port** &mdash; порт
    * **label_selector_results** &mdash; список значений *label_selector*'ов, установленных в запросе ("null", если у *endpoint*'а метки с таким путем нет)

### Получение списка *pod*'ов

### Запрос
Можно сделать, передав proto message `TReqResolvePods`, описанный в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto), в метод `resolve_pods`:
```py
from infra.yp_service_discovery.api import api_pb2
...
request = api_pb2.TReqResolvePods()
request.cluster_name = 'sas'
request.pod_set_id = 'chaos-service-slave'
request.client_name = 'chaos-service-resolver:{}'.format(socket.gethostname())
request.ruid = 'resolve-chaos-service-in-sas'

result = resolver.resolve_pods(request)
```

`TRspResolvePods`:
* **cluster_name** (required) &mdash; имя YP кластера
* **pod_set_id** (required) &mdash; идентификатор *pod_set*'а
* **client_name** &mdash; имя пользователя для идентификации на стороне YP Service Discovery; перезаписывает значение **client_name**, установленное при инициализации `Resolver`
* **ruid** &mdash; произвольная строка для идентификации запроса, значение будет установлено в поле **ruid** в ответе

### Ответ
Возвращается в виде proto-сообщения `TRspResolvePods`, определенного в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto),
* **timestamp** &mdash; YP timestamp версии данных
* **pod_set** &mdash; `TPodSet`
* **resolve_status** &mdash; статус `NOT_EXISTS` (*endpoint_set*'а не существует), `NOT_CHANGED` (*DEPRECATED*), `OK`
* **host** &mdash; имя хоста YP Service Discovery, с которого пришел ответ
* **ruid** &mdash; равен **ruid** из запроса или рандомному значению, если **ruid** не был передан

`TPodSet`:
* **pod_set_id** &mdash; идентификатор *endpoint_set*'а
* **pods** &mdash; список *pod*'ов (`TPod`)
    * **id** &mdash; идентификатор *pod*'а
    * **node_id** &mdash; идентификатор ноды на которую зашедулен *pod*
    * **dns** &mdash; *dns* ('Tpod.TDns')
        * **persistent_fqdn** &mdash; постоянный fqdn *pod*'а
        * **persistent_fqdn** &mdash; временный fqdn *pod*'а который зависит от ноды на которую зашедулен *pod*
    * **ip6_address_allocations** &mdash; список объектов ('TPod.TIP6AddressAllocation')
    * **ip6_subnet_allocations** &mdash; список объектов ('TPod.TIP6SubnetAllocation')
