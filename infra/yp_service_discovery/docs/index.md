# Документация YP Service Discovery

Пока здесь только копия страницы на вики [https://wiki.yandex-team.ru/yp/discovery/usage/](https://wiki.yandex-team.ru/yp/discovery/usage/). Будем облагораживать.

## Support Chat

Все вопросы стоит задавать [в чате](https://t.me/joinchat/FUB5vgmFaIpFg-XK).

## Основные понятия
* [https://wiki.yandex-team.ru/yp/discovery/](https://wiki.yandex-team.ru/yp/discovery/)
* [https://wiki.yandex-team.ru/yp/YP-Quick-start-guide/#yp.sd](https://wiki.yandex-team.ru/yp/YP-Quick-start-guide/#yp.sd)

## Адреса YP Service Discovery
* `sd.yandex.net`, есть также полокационные балансеры: `{sas,man,vla,msk}.sd.yandex.net`
* HTTP порт `8080`, gRPC порт `8081`

### Доступы
Правила фаервола: [Панчер](https://puncher.yandex-team.ru/?destination=sd.yandex.net&rules=exclude_rejected&values=all&sort=destination).

## Протокол работы

YP Service Discovery поддерживает протоколы HTTP и gRPC.

Структура запроса `TReqResolveEndpoints` и ответа `TRspResolveEndpoints` YP Service Discovery описана в [infra/yp_service_discovery/api/api.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/api/api.proto). [Подробное описание](#request-desc).

### Ручки
Путь | gRPC | HTTP
:--- | :--- | :---
`/resolve_endpoints` | Запрос: `TReqResolveEndpoints`. Ответ: `TRspResolveEndpoints`. | Запрос: proto-сообщение `TReqResolveEndpoints` в сериализованном виде. Ответ: proto-сообщение `TRspResolveEndpoints` в сериализованном виде.
`resolve_endpoints/json` | - | Запрос: `TReqResolveEndpoints` в формате json. Ответ: `TRspResolveEndpoints` в формате json.

### Запрос

{% code '/infra/yp_service_discovery/api/api.proto' lang='protobuf' lines='[BEGIN TReqResolveEndpoints]-[END TReqResolveEndpoints]' %}

**Имя поля** | **Тип** | **Описание**
:--- | :--- | :---
`cluster_name` | required | имя YP кластера запрашиваемого endpoint set'а (`sas-test`, `sas`, `man-pre`, `man`, `vla`, `iva`, `myt`, `xdc`)
`endpoint_set_id` | required | идентификатор endpoint set'а
`client_name` | required | имя пользователя (Вас) для идентификации на стороне YP Service Discovery
`label_selectors` | optional | список путей в `/labels`, по которым нужно получить значения для каждого endpoint'а
`watch_token` | deprecated | не устанавливать
`ruid` | optional | произвольная строка для идентификации запроса, значение будет установлено в поле `ruid` в ответе
`endpoint_set_label_selectors` | optional | список путей в `/labels`, по которым нужно получить значения для каждого endpoint set'а


### Ответ

{% code '/infra/yp_service_discovery/api/api.proto' lang='protobuf' lines='[BEGIN TRspResolveEndpoints]-[END TRspResolveEndpoints]' %}

**Имя поля** | **Описание**
:--- | :---
`timestamp` | версия данных (YP timestamp)
`endpoint_set` | структура `TEndpointSet`; содержит идентификатор endpoint set'а и списка endpoint'ов
`resolve_status` | `enum EEndpointResolveStatus`; статус резолва
`watch_token` | не используется
`host` | имя хоста YP Service Discovery, с которого пришел ответ
`ruid` | равен `ruid` из запроса или рандомному значению, если `ruid` не был передан


{% code '/infra/yp_service_discovery/api/api.proto' lang='protobuf' lines='[BEGIN EResolveStatus]-[END EResolveStatus]' %}

**Значение** | **Описание**
:--- | :---
0 | `NOT_EXISTS`: endpoint set не существует
1 | `NOT_CHANGED`: не используется
2 | `OK`: endpoint set существует и имеет непустой список endpoint'ов
3 | `EMPTY`: endpoint set существует и имеет пустой список endpoint'ов

{% code '/infra/yp_service_discovery/api/api.proto' lang='protobuf' lines='[BEGIN TEndpointSet]-[END TEndpointSet]' %}


**Имя поля** | **Описание**
:--- | :---
`endpoint_set_id` | идентификатор endpoint set'а
`endpoints` | список endpoint'ов
`label_selector_results` | список значений запрошенных endpoint_set_label_selector'ов; "null", если у endpoint set'а нет соответствующей метки

{% code '/infra/yp_service_discovery/api/api.proto' lang='protobuf' lines='[BEGIN TEndpoint]-[END TEndpoint]' %}

**Имя поля** | **Описание**
:--- | :---
`id` | идентификатор endpoint'а
`protocol` | протокол: UDP или TCP
`fqdn` | переменный fqdn
`ip4_address` | IPv4 адрес
`ip6_address` | IPv6 адрес
`port` | порт
`label_selector_results` | список значений запрошенных label_selector'ов; "null", если у endpoint'а нет соответствующей метки
`ready` | для подов под контролем Pod Agent (Y.Deploy): `true`, если статус пода равен `ready` и `target_state` не равен `removed` или `suspended` ([подробнее](https://deploy.yandex-team.ru/docs/concepts/pod/workload/probes#readiness-proba)); для остальных подов (Nanny): `true`, если `current state` или `target state` равен `ACTIVE`

{% note info %}

На данный момент в ответе ручки `/resolve_endpoints/json` поля, значения которых равны default-значению типа, не пишутся. Так, например, `resolve_status: 0` опускается.

{% endnote %}

### Пример запроса
``` bash
curl "http://sd.yandex.net:8080/resolve_endpoints/json" \
    --data '{"cluster_name": "sas", "endpoint_set_id": "chaos-service", "client_name": "dima-zakharov", "ruid": "resolve_chaos_service_in_sas_1"}'
```

Ответ:
``` json
{
    "timestamp": 1678834452869939500,
    "endpoint_set": {
        "endpoint_set_id": "chaos-service",
        "endpoints": [
            {
                "id": "1x2vczbykk1c1z1e",
                "protocol": "TCP",
                "fqdn": "p4y2whtnowhbm2w3.sas.yp-c.yandex.net",
                "ip6_address": "2a02:6b8:c14:3f1e:10d:bd77:4801:0",
                "port": 3388
            }
        ]
    },
    "resolve_status": 2,
    "watch_token": "0",
    "host": "myt1-1486-msk-yp-service-discovery-20075.gencfg-c.yandex.net",
    "ruid": "resolve_chaos_service_in_sas_1"
}
```

### Коды ответа
ситуация | HTTP код ответа | gRPC код ответа | resolve_status
:--- | :--- | :--- | :---
не указан cluster | 400 Bad request | INVALID_ARGUMENT | -
не указан client_name | 405 Method not allowed | UNAUTHENTICATED | -
ошибка на бекенде | 500 Internal Server Error | INTERNAL | -
endpoint set не существует | 200 OK (будет 404, YP-1163) | OK | NOT_EXISTS (0)
endpoint set существует, список endpoint'ов пуст | 200 OK | OK | EMPTY (2)
endpoint set существует, список endpoint'ов не пуст | 200 OK | OK | OK (2)

{% note warning %}

Реплики в SD являются полностью независимыми, поэтому разные инстансы могут отдавать данные за разные моменты времени, для сервисов это может выглядеть как моргание данных. Обязательно нужно учитывать timestamp и забирать только более новые данные.

{% endnote %}

{% note warning %}

Если Вы имплементируете свою библиотеку, то не забудьте кешировать ответы SD на диск. Используйте закешированные результаты в случае проблем с резолвом через SD. Адрес `sd.yandex.net` тоже стоит сохранять на случай проблем с резолвом адреса балансера.

{% endnote %}

## Библиотеки
### C++
#### sdlib

{% note tip %}

Рекомендуется использовать именно эту библиотеку. Она поддерживает обновление endpoint set-ов в бэкграунде, сохранение результатов на диск (кеширование), правильно обрабатывает ответы YP SD (например, учитывает timestamp в ответе).

{% endnote %}

Код в Аркадии: [infra/yp_service_discovery/libs/sdlib](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/libs/sdlib)

#### gRPC resolver
Код в Аркадии: [infra/yp_service_discovery/resolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/resolver)

### Python
#### gRPC resolver
Код в Аркадии: [infra/yp_service_discovery/python/resolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/python/resolver)

### Java
#### gRPC resolver
Код в Аркадии: [infra/yp_service_discovery/java](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/java)

### Golang
#### gRPC resolver
Код в Аркадии: [infra/yp_service_discovery/golang/resolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver)

