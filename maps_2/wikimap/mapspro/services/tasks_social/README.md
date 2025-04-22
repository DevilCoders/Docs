# wiki-tasks-social

Фоновые и асинхронные задачи социальной части Народной Карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_social |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-social/ |
| Проект в CI | [maps-core-nmaps-tasks-social](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-social/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_social) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_social/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_social_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_social_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_social_unstable/)

## Documentation

Различные cron и grinder-воркеры, запускаемые пользователями вручную или по расписанию.


## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_SOCIAL_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-social` | `_PGAASINTERNALNETS_`:6432,27018 |
| `wiki-tasks-social` | `storage-int.mds.yandex.net`:80,443,1111 |
| `wiki-tasks-social` | `_MAPS_CORE_ZOOKEEPER_STABLE_RTC_NETS_`:2181 |
| `wiki-tasks-social` | `_YTNETS_`:80,443,9013 |
| `wiki-tasks-social` | `hahn.yt.yandex.net`:80,443 |
| `wiki-tasks-social` | `sqs.yandex.net`:8771 |


## ecstatic Datasets

Нет

## What happens when service is down

В Народной Карте перестанут выполняться часть асинхронных задач.


## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_social_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_social_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_social_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_social_unstable |


## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-social-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-social-stable-panel-main) |
| Testing | [maps-core-nmaps-tasks-social-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-social-testing-panel-main) |
| Unstable | [maps-core-nmaps-tasks-social-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-social-unstable-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |
| database | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | daemon/grinder/cron | URL/path |
|---|---|---|
| wiki-assessment-sampler | cron | /var/log/yandex/maps/wiki/assessment/sampler.log* |
| wiki-auto-mailer | cron | /var/log/yandex/maps/wiki/auto-mailer/* |
| wiki-badge-worker | grinder | /var/log/yandex/maps/wiki/badge/* |
| wiki-involvement-stats-worker | daemon(pubsub) | /var/log/yandex/maps/wiki/involvement-stats/* |
| wiki-notifications-dispatcher | cron | /var/log/yandex/maps/wiki/notifications_dispatcher/* |
| wiki-rating-worker | cron(pubsub) | /var/log/yandex/maps/wiki/rating/* |
| wiki-social-cleaner | cron | /var/log/yandex/maps/wiki/social/cleaner.* |
| wiki-stats-updater | daemon(pubsub) | /var/log/yandex/maps/wiki/stats-updater/* |
| wiki-update-badges-worker | cron | /var/log/yandex/maps/wiki/update-badges/* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет

