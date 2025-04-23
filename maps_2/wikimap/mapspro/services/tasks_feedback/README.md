# wiki-tasks-feedback

Обработка фидбека в Народной Карте

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Денис Зверев ( miror@yandex-team.ru ) Алексей Градсков ( gradksov@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_feedback |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-feedback/ |
| Проект в CI | [maps-core-nmaps-tasks-feedback](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-feedback/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_feedback) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_feedback/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_feedback_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_feedback_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_feedback_unstable/)

## Documentation

Кроновские задания и grinder-worker'ы для обработки федбэка в НК

[Документация на Wiki](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/wikinktasks_cur/#boleedetalnyeopisanijakomponent)

## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_FEEDBACK_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-feedback` | `_PGAASINTERNALNETS_`:6432,27018 |
| `wiki-tasks-feedback` | `core-nmaps-editor.maps.yandex.net`:80 |
| `wiki-tasks-feedback` | `core-nmaps-social.maps.yandex.net`:80 |
| `wiki-tasks-feedback` | `feedback-int.c.maps.yandex.net`:80 |
| `wiki-tasks-feedback` | `st-api.yandex-team.ru`:443 |
| `wiki-tasks-feedback` | `_MAPS_CORE_ZOOKEEPER_STABLE_RTC_NETS_`:2181 |
| `wiki-tasks-feedback` | `_YTNETS_`:80,443,9013 |
| `wiki-tasks-feedback` | `hahn.yt.yandex.net`:80,443 |
| `wiki-tasks-feedback` | `sqs.yandex.net`:8771 |


## ecstatic Datasets

Нет

## What happens when service is down

Фидбэк Народной Карты перестанет обрабатываться

## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_feedback_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[Ошибки в синхронизациии с Трекером](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/tasks/ST-and-FBAPI-sync-workers/#vozmozhnyenepoladkivsinxronizaciistrekerom)

[Ошибки в синхронизации с FBAPI](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/tasks/ST-and-FBAPI-sync-workers/#vozmozhnyenepoladkivsinxronizaciisfbapi)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_feedback_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_feedback_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_feedback_unstable |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-feedback-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-feedback-stable-panel-main) |
| Testing | [maps-core-nmaps-tasks-feedback-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-feedback-testing-panel-main) |
| Unstable | [maps-core-nmaps-tasks-feedback-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-feedback-unstable-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |
| database | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |
| database | [mapspro_view_trunk](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbhqds4cpsr293br2t3;dbname=mapspro_view_trunk) |
| database | [mapspro_validation](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3aee79ba-6480-4d9d-88d8-020585c701b3;dbname=mapspro_validation) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | cron/grinder/daemon | URL/path |
|---|---|---|
| wiki-feedback-set-deployed-worker | cron | /var/log/yandex/maps/wiki/feedback-set-deployed/* |
| wiki-guide-pedestrian-worker | grinder | /var/log/yandex/maps/wiki/guide-pedestrian/* |
| wiki-import-feedback-worker | grinder | /var/log/yandex/maps/wiki/import-feedback/* |
| wiki-import-indoor-feedback-worker | cron | /var/log/yandex/maps/wiki/import-indoor-feedback/* |
| wiki-matview-refresher-worker | cron | /var/log/yandex/maps/wiki/matview-refresher/* |
| wiki-releases-notification-worker | grinder | /var/log/yandex/maps/wiki/releases_notification/* |
| wiki-notifications-sender | daemon | /var/log/yandex/maps/wiki/notifications-sender/* |
| wiki-reject-feedback-worker | grinder | /var/log/yandex/maps/wiki/reject_feedback/* |
| wiki-route-lost-feedback-worker | cron | /var/log/yandex/maps/wiki/route_lost_feedback/* |
| wiki-schedule-feedback-worker | cron | /var/log/yandex/maps/wiki/schedule-feedback/* |
| wiki-sprav-pedestrian-feedback | cron (3) | /var/log/yandex/maps/wiki/sprav-pedestrian-feedback/* |
| wiki-sync-fbapi-feedback-worker | cron | /var/log/yandex/maps/wiki/sync-fbapi-feedback/* |
| wiki-validation-feedback-converter-worker | grinder | /var/log/yandex/maps/wiki/validation_feedback_converter/* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет
