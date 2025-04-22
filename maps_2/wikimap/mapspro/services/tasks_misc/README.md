# wiki-tasks-misc

Асинхронные пользовательские задачи Народной Карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Алексей Пономарев ( ponomarev@yandex-team.ru ) Борис Чикунов ( chikunov@yandex-team.ru ) Сергей Ливерко ( mr-spock@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_misc |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-misc/ |
| Проект в CI | [maps-core-nmaps-tasks-misc](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-misc/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_misc) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_misc/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_misc_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_misc_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_misc_unstable/)

## Documentation

Различные grinder-воркеры, запускаемые пользователями вручную или по расписанию.


## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_MISC_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-misc` | `_PGAASINTERNALNETS_`:6432,27018 |
| `wiki-tasks-misc` | `storage-int.mds.yandex.net`:80,443,1111 |
| `wiki-tasks-misc` | `_MAPS_CORE_ZOOKEEPER_STABLE_RTC_NETS_`:2181 |
| `wiki-tasks-misc` | `core-nmaps-tasks.maps.yandex.net`:80 |


## ecstatic Datasets

Нет

## What happens when service is down

В Народной Карте перестанут выполняться часть асинхронных задач, особенно таких как импорт данных или создание релизной ветки.


## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_misc_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_misc_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_misc_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_misc_unstable |


## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-misc-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-misc-stable-panel-main) |
| Testing | [maps-core-nmaps-tasks-misc-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-misc-testing-panel-main) |
| Unstable | [maps-core-nmaps-tasks-misc-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-misc-unstable-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |
| database | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |
| database | [mapspro_view_trunk](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbhqds4cpsr293br2t3;dbname=mapspro_view_trunk) |
| database | [mapspro_view_trunk_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbsj61vh1ob68181o6v;dbname=mapspro_view_trunk_labels) |
| database | [mapspro_view_stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbe9n7jsv7p2rih4na2;dbname=mapspro_view_stable) |
| database | [mapspro_view_stable_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb4cb8nj54at9gqh3jf;dbname=mapspro_view_stable_labels) |
| database | [mapspro_validation](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3aee79ba-6480-4d9d-88d8-020585c701b3;dbname=mapspro_validation) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | grinder/tool | URL/path |
|---|---|---|
| wiki-editor-tool | tool | /usr/lib/yandex/maps/wiki/bin/wiki-editor-tool --help |
| wiki-apply-shadow-attributes-worker | grinder | /var/log/yandex/maps/wiki/apply_shadow_attributes/* |
| wiki-groupedit-worker | grinder | /var/log/yandex/maps/wiki/groupedit/* |
| wiki-import-worker | grinder | /var/log/yandex/maps/wiki/import/* |
| wiki-prepare-stable-branch-worker | grinder | /var/log/yandex/maps/wiki/prepare_stable_branch/* |
| wiki-vrevisions-refresh-worker | grinder | /var/log/yandex/maps/wiki/vrevisions-refresh/* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет

