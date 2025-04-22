# Endpoints resolver via YP Service Discovery
Библиотека для получения *endpoint*'ов сервиса с помощью YP Service Discovery.

Список *endpoint*'ов можно получить, зная идентификатор *endpoint_set*'а и имя YP кластера.

### Важно иметь в виду
* Реплики в YP SD являются полностью независимыми, поэтому разные инстансы могут отдавать данные за разные моменты времени. Обязательно нужно учитывать **timestamp** и забирать только более новые данные.

### TResolver
`TResolver::TResolver`:
* **clientName** &mdash; имя пользователя для идентификации на стороне YP Service Discovery; желательно также передать имя хоста, с которого совершается запрос; на запросы с пустым **clientName** YP SD отвечает пустым ответом
* **address** &mdash; gRPC адрес YP Service Discovery; это **sd.yandex.net:8081**, также есть полокационные балансеры **{sas,man,vla,msk}.sd.yandex.net:8081**.
* **timeout** &mdash; таймаут на запрос; если достигается, бросается исключение `yexception`.

```
#include <infra/yp_service_discovery/resolver/resolver.h>
...
NServiceDiscovery::TResolver resolver("test:" + HostName(),
                                      NServiceDiscovery::SERVICE_DISCOVERY_GRPC_ADDRESS,
                                      TDuration::Seconds(5));
```

### Запрос
Можно сделать, просто задав имя кластера и идентификатор *endpoint_set*'а:
```
auto result = resolver.Resolve("sas", "chaos-service-slave");
```
или, передав proto message `NYP::NServiceDiscovery::NApi::TReqResolveEndpoints`, описанный в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto),
```
#include <infra/yp_service_discovery/api/api.pb.h>
...
NYP::NServiceDiscovery::NApi::TReqResolveEndpoints request;
request.set_cluster_name("sas");
request.set_endpoint_set_id("chaos-service-slave");
request.set_client_name("chaos-service-resolver:" + HostName());
request.add_label_selectors("path/to/label");
request.set_ruid("resolve-chaos-service-in-sas");

auto result = resolver.Resolve(request);
```

Также есть методы для получения списка *endpoint*'ов сразу для множества *endpoint_set*'ов, в которых списки `endpoint_set_id` или `TReqResolveEndpoints` передаются в контейнере`TVector`.

`NYP::NServiceDiscovery::NApi::TRspResolveEndpoints`:
* **cluster_name** (required) &mdash; имя YP кластера
* **endpoint_set_id** (required) &mdash; идентификатор *endpoint_set*'а
* **client_name** &mdash; имя пользователя для идентификации на стороне YP Service Discovery; перезаписывает значение **clientName**, установленное при инициализации `TResolver`
* **label_selectors** &mdash; список путей в `/labels`, по которым нужно получить значения
* **watch_token** &mdash; *DEPRECATED*
* **ruid** &mdash; произвольная строка для идентификации запроса, значение будет установлено в поле **ruid** в ответе

### Ответ
Возвращается в виде proto-сообщения `NYP::NServiceDiscovery::NApi::TRspResolveEndpoints`, определенного в файле [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto),
* **timestamp** &mdash; YP timestamp версии данных
* **endpoint_set** &mdash; `NYP::NServiceDiscovery::NApi::TEndpointSet`
* **resolve_status** &mdash; статус `NOT_EXISTS` (*endpoint_set*'а не существует), `NOT_CHANGED` (*DEPRECATED*), `OK`
* **watch_token** &mdash; *DEPRECATED*
* **host** &mdash; имя хоста YP Service Discovery, с которого пришел ответ
* **ruid** &mdash; равен **ruid** из запроса или рандомному значению, если **ruid** не был передан

`NYP::NServiceDiscovery::NApi::TEndpointSet`:
* **endpoint_set_id** &mdash; идентификатор *endpoint_set*'а
* **endpoints** &mdash; список *endpoint*'ов (`NYP::NServiceDiscovery::NApi::TEndpoint`)
    * **id** &mdash; идентификатор *endpoint*'а
    * **protocol** &mdash; протокол подключения (TCP или UDP)
    * **fqdn** &mdash; переменный fqdn
    * **ip4_address** &mdash; IPv4 адрес
    * **ip6_address** &mdash; IPv6 адрес
    * **port** &mdash; порт
    * **label_selector_results** &mdash; список значений *label_selector*'ов, установленных в запросе ("null", если у *endpoint*'а метки с таким путем нет)
