# Динамические зоны в YP DNS

Динамическими зонами называются зоны, управляемые через Zones Manager, который внедрен в [Бридж](../yp_dns_api/api.md).
Их можно "на лету" создавать, удалять и менять, а все сервисы без перезапуска автоматически их подтянут.

Эта статья скорее техническая и описывает детали реализации управления и хранения динамических зон.
Поэтому для пользователей достаточно прочитать только [документацию к API](../yp_dns_api/api.md#list-zones) для управления зон.

Начнем мы с описания записи о зоне, затем перейдем к тому, как работает Zones Manager (core-компонент для работы с зонами), и закончим тем, как сервисы работают с динамическими зонами.

## Зона как объект в YP

Для хранения записи о зоне используется кластер YP-XDC.
Каждая зона представлена в виде объекта типа [dns_zone](https://a.yandex-team.ru/arcadia/yp/yp_proto/yp/client/api/proto/dns_zone.proto).

Главное в объекте `dns_zone` поле `/spec/config`, в котором хранится конфигурация зоны.
Этот конфиг несколько отличается от [конфига TZoneConfig](../yp_dns_api/api.md#zone-config), который используется в сервисах,
но между ними можно провести взаимно однозначное соответствие:
[NYpDns::TZoneConfig -> YP::TDnsZoneConfig](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/zone/zone.cpp?rev=r9516735#L222) и обратно [YP::TDnsZoneConfig -> NYpDns::TZoneConfig](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/zone/zone.cpp?rev=r9516735#L16).

Также используются лейблы `/labels`. Пример значений лейблов для одной из зон:

```json
"labels": {
    "yp_dns": {
        "enable": true              // Включена ли зона для использования на DNS-сервере (Unbound)
    },
    "owners": [                     // Список пользователей, которые добавляются в овнеры dns_record_set-ов
        "robot-ypdnsapi",
        "robot-ypdnsapi-repl"
    ],
    "state": {
        "target_state": "CREATED",  // Целевое состояние зоны
        "current_state": "CREATED"  // Текущее состояние зоны
    },
    "yp_dns_export": {
        "timestamp": 1653488470     // Время, когда DNS Export обновил /labels/yp_dns/enable
    }
}
```

Поле `/labels/yp_dns` управляется сервисом YP DNS Export, который решает включать ли зону для использования на DNS-серверах или нет.
Читают это поле, соответственно, DNS-серверы: если там выставлено `enable: false`, то запросы по доменам в данной зоне не обрабатываются.
Также YP DNS Export пишет поле `/labels/yp_dns_export`, где хранит разную метаинаформацию (например, таймстемп последнего обновления) для себя.

Поле `/labels/owners` задает список пользователей (логины), которые будут добавляться в ACL dns_record_set-ов при их [создании в Бридже](../yp_dns_api/api.md#update-records).

В поле `/labels/state` поддерживается текущий и целевой статус зоны, это делает Zones Manager (о нем ниже).
На основе `/labels/state/target_state` определяется, кто может читать зону, использовать ее.
Значение `/labels/state/current_state` же говорит о том, в каком сейчас состоянии зона.
Если значение `current_state` не равно значению `target_state`, от это значит, что зона в сейчас в состоянии перехода.
Если же значения равны, то зона успешно перешла в запрошенное состояние.
О том, какие бывают состояния зоны и как зона переходит из одного в другое, читайте ниже.

## Управление зонами изнутри: Zones Manager

За всю работу с динамическими зонами отвечает [Zones Manager](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/dynamic_zones/zones_manager.h) (далее просто Менеджер).
Он целиком с API встроен Бридж через [Zones Manager Service](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/dynamic_zones/zones_manager_service),
за счет этого все операции с зонами можно [делать через Бридж](../yp_dns_api/api.md#list-zones).

### State Coordinator

Прежде чем перейти к описанию работы методов Менеджера, нужно ознакомиться с одной из ключевых частей Менеджера - [State Coordinator](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_state_coordinator.h) (далее просто Координатор).
Эта сущность отвечает за определение статусов зон (`dns_zone:/labels/state`), а также за то, какой сервис может знать о какой зоне (например, для метода `ListZonesForService` Менеджера).

Есть основная реализация Координатора - [TZonesStateCoordinator](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_state_coordinator.h?rev=r9460342#L104). Пока тут нет текстового описания, можно почитать его код.

### Создание зоны

Создание зоны для Менеджера заключается в том, чтобы создать объект `dns_zone` в YP.
Перед этим он запрашивает статус зоны у Координатора (при создании статус будет таким: `{current_state: NOT_EXIST, target_state: CREATED}`), который затем установит в `/labels/state`.
На самом деле, Менеджер делает это на любое изменение зоны.

### Удаление зоны

При запросе на удаление Менеджер просто удаляет объект зоны из YP.
Таким образом, зона сразу пропадает.
Однако записи ее при этом не удаляются и не изменяются, поэтому перед удалением стоит самостоятельно удостовериться, что записей в зоне больше нет.

### Получение списка зон

Чтобы запросить список зон, пользователь передает свой идентификатор [`service_type`](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto?rev=r9460342#L9), который является строкой (список возможных значений зафиксирован Координатором).
Дальше Менеджер получает список всех зон с их конфигурациями через запрос к реплике с зонами или через запрос в YP.
Однако по алгоритму Координатора может быть так, что в ответе нужно вернуть не все зоны, а только те, которые на данный момент доступны запрошенному `service_type`.
Поэтому дальше Менеджер фильтрует список зон, оставляя только те, что Координатор опредилил как "готовые" для данного сервиса (метод [`IsZoneReadyForService`](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_state_coordinator.h?rev=r9549488#L54)).

Также помимо динамических зон можно в ответ добавить какой-то список статических зон, записанных в [конфиг Менеджера](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/protos/configs/zones_manager.proto?rev=r9116163#L33).
Делать это или нет опять же решает Координатор (метод [`NeedStaticZones`](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_state_coordinator.h?rev=r9549488#L56)).

### Обновление зоны

Менеджер также поддерживает обновление конфигурации зоны, через метод `TZonesManager::UpdateZone`.
Но метода в API для обновления конфигурации зоны нет, поэтому фактически он сейчас не используется.

### Обновление current-статуса зон

Помимо задач на выполнение запросов от пользователей Менеджер также имеет в своей ответственности задачу по обновлению текущего статуса зоны `/labels/state/current_state`.
Для этого он периодически собирает статусы всех зон при помощи Координатора и обновляет соответствующее поле в YP-объекте зоны, если статус изменился.
Целевой статус при этом он не меняет, `target_state` меняется только при определенных запросах от пользователей (например, при создании зоны).

## Ссылки

- Код управления динамическими зонами: [infra/libs/yp_dns/dynamic_zones](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/dynamic_zones)
- Описание конфига зоны `TZoneConfig`: [infra/libs/yp_dns/zone/protos/config.proto](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/zone/protos/config.proto)
- Описание объекта в YP для DNS-зоны: [yp/yp_proto/yp/client/api/proto/dns_zone.proto](https://a.yandex-team.ru/arcadia/yp/yp_proto/yp/client/api/proto/dns_zone.proto)
- Задачи, где все начиналось: [TRAFFIC-11685](https://st.yandex-team.ru/TRAFFIC-11685), [YP-3251](https://st.yandex-team.ru/YP-3251)
