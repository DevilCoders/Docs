# wiki-tasks-sprav

Интеграция Народной Карты и Справочника

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Евклид Никифоров ( euclid@yandex-team.ru ) Сергей Ливерко ( mr-spock@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-sprav/ |
| Проект в CI | [maps-core-nmaps-tasks-sprav](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-sprav/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_sprav) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_sprav/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_sprav_stable/)

## Documentation

Обмен данными между Народной Картой и Справочником

Сервис состоит из двух процессов:
* [export_poi_worker](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav/src/export_poi_worker/README.md)
* [merge_poi_worker](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav/src/merge_poi_worker/README.md)


Заливка фоток/гипотез от пешеходов в MRC/НК:
* [walkers_export_downloader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav/src/walkers_export_downloader/README.md)
* [yang_downloader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav/src/yang_downloader/README.md)


## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_SPRAV_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-sprav` | `_PGAASINTERNALNETS_`:6432 |
| `wiki-tasks-sprav` | `core-nmaps-editor.maps.yandex.net`:80 |
| `wiki-tasks-sprav` | `core-nmaps-editor-writer.maps.yandex.net`:80 |
| `wiki-tasks-sprav` | `core-nmaps-social.maps.yandex.net`:80 |
| `wiki-tasks-sprav` | `sandbox.yandex-team.ru`:80,443 |
| `wiki-tasks-sprav` | `storage-int.mds.yandex.net`:80,443,1111 |
| `wiki-tasks-sprav` | `upload.stat.yandex-team.ru`:80,443 |
| `wiki-tasks-sprav` | `_YTNETS_`:80,443,9013 |
| `wiki-tasks-sprav` | `hahn.yt.yandex.net`:80,443 |
| `wiki-tasks-sprav` | `yang.yandex-team.ru`:443 |
| `wiki-tasks-sprav` | `core-nmaps-mrc-agent-proxy.maps.yandex.net`:80 |


## ecstatic Datasets

Нет

## What happens when service is down

В Народной Карте и Справочнике перестанут синхронизироваться данные

## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_sprav_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_sprav_stable |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-sprav-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-sprav-stable-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |
| database | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | daemon/cron/tool | URL/path |
|---|---|---|
| json2ymapsdf | tool | /usr/bin/json2ymapsdf --help |
| wiki-export-poi-worker | cron | /var/log/yandex/maps/wiki/export-poi/* |
| wiki-merge-poi-worker | cron | /var/log/yandex/maps/wiki/merge-poi/* |
| wiki-toloka-downloader | cron | /var/log/yandex/maps/wiki/toloka-downloader/* |
| wiki-walkers-export-downloader | cron | /var/log/yandex/maps/wiki/walkers-export-downloader/* |
| wiki-yang-downloader | cron | /var/log/yandex/maps/wiki/yang-downloader/* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет

