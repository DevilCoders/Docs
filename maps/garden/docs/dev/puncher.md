# Сетевые доступы

## Сетевые доступы для задач в YT

Контейнеры с задачами в YT запускаются с дополнительной изоляцией сети. Для изоляции
используется сетевые макросы:
- стабильный контур: `_YT_JOBS_MAPS_CORE_GARDEN_STABLE_NETS_` [puncher](https://puncher.yandex-team.ru/?source=_YT_JOBS_MAPS_CORE_GARDEN_STABLE_NETS_&rules=exclude_rejected&values=all&sort=source) (`project_id=f41a`, фигурирует в ipv6-адресах изолированных порто-контейнеров, [racktables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_YT_JOBS_MAPS_CORE_GARDEN_STABLE_NETS_))
- datatesting контур: `_YT_JOBS_MAPS_CORE_GARDEN_DATATESTING_NETS_` [puncher](https://puncher.yandex-team.ru/?source=_YT_JOBS_MAPS_CORE_GARDEN_DATATESTING_NETS_&rules=exclude_rejected&values=all&sort=source) (`project_id=f41b`, фигурирует в ipv6-адресах изолированных порто-контейнеров, [racktables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_YT_JOBS_MAPS_CORE_GARDEN_DATATESTING_NETS_))
- пользовательские контуры: `_YT_JOBS_MAPS_CORE_GARDEN_UNSTABLE_NETS_` [puncher](https://puncher.yandex-team.ru/?source=_YT_JOBS_MAPS_CORE_GARDEN_UNSTABLE_NETS_&rules=exclude_rejected&values=all&sort=source) (`project_id=f41c`, фигурирует в ipv6-адресах изолированных порто-контейнеров, [racktables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_YT_JOBS_MAPS_CORE_GARDEN_UNSTABLE_NETS_))

Для этого в спеке операции указывается параметр `network_project=maps_core_garden_*`.
Для дочерних операций так же указывается параметр `network_project`.

### Доступы до общеяндексовских ресурсов:
Изначально доступы заказывались в тикете [MAPSGARDEN-18614](https://st.yandex-team.ru/MAPSGARDEN-18614):
* [S3](https://wiki.yandex-team.ru/mds/s3-api/#xosty/port)
* [MDS](https://wiki.yandex-team.ru/mds/dev/protocol/#xosty)
* [Sandbox](https://wiki.yandex-team.ru/sandbox/firewall/)
* [Ecstatic](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#firewallports)
* [YT-кластера](https://docs.yandex-team.ru/yt/gettingstarted#puncher) hahn и locke
* [YQL](https://yql.yandex-team.ru/docs/yt/interfaces/http/)
* [JNS](https://jns.yandex-team.ru)

Остальные доступы необходимо явно заказывать в панчере для сетевых макросов.

## Сетевые доступы для сервера
Серверу необходимы доступы до сервисов, на которых хранятся данные для удаления ресурсов.
