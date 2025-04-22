# wiki-tasks-export

Экспорт данных из Народной Карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Евклид Никифоров ( euclid@yandex-team.ru ) Виталий Титов ( uht@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_export |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-export/ |
| Проект в CI | [maps-core-nmaps-tasks-export](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-export/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_export) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_export/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_export_testing/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_export_stable/)

## Documentation

Экспорт данных:
- сервисные объекты - картографам
- основные объекты - датасеты по регионам в Огород
- масстранзит - датасет для общественного транспорта

Пакетный экспорт, см. [readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_export/src/validation_export_worker/README.md)


## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_EXPORT_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-export` | `_PGAASINTERNALNETS_`:6432,27018 |
| `wiki-tasks-export` | `storage-int.mds.yandex.net`:80,443,1111 |
| `wiki-tasks-export` | `_MAPS_CORE_ZOOKEEPER_STABLE_RTC_NETS_`:2181 |
| `wiki-tasks-export` | `core-nmaps-tasks.maps.yandex.net`:80 |


## ecstatic Datasets

- yandex-maps-geodata6


## What happens when service is down

Из Народной Карты не будут экспортироваться данные, свежие данные не будут процесситься в Огороде и т.д.


## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_export_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_export_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_export_testing |


## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/


## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-export-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-export-stable-panel-main) |
| Testing | [maps-core-nmaps-tasks-export-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-export-testing-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | daemon/cron/tool | URL/path |
|---|---|---|
| json2ymapsdf | tool | /usr/bin/json2ymapsdf --help |
| wiki-export-worker | daemon (grinder) | /var/log/yandex/maps/wiki/export/* |
| wiki-validation-export-worker | daemon (grinder) | /var/log/yandex/maps/wiki/validation-export/* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет

