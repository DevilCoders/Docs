# wiki-tasks-yt

Запуск задач Народной Карты в YT

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Алексей Пономарев ( ponomarev@yandex-team.ru ) Борис Чикунов ( chikunov@yandex-team.ru ) Евклид Никифоров ( euclid@yandex-team.ru ) Сергей Ливерко ( mr-spock@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_yt |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-yt/ |
| Проект в CI | [maps-core-nmaps-tasks-yt](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-yt/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_yt) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_yt/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_yt_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_yt_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_yt_unstable/)

## Documentation

Grinder-воркеры принимают задачу, запускают себя в YT асинхронно (c++ бинарь, vanilla).
Результат и статус задачи пишут в базу yt-job.

## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_YT_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source| Destination |
|---|---|
| `wiki-tasks-yt` | `_PGAASINTERNALNETS_`:6432,27018 |
| `wiki-tasks-yt` | `_MAPS_CORE_ZOOKEEPER_STABLE_RTC_NETS_`:2181 |
| `wiki-tasks-yt` | `core-nmaps-editor.maps.yandex.net`:80 |
| `wiki-tasks-yt` | `_YTNETS_`:80,443,9013 |
| `wiki-tasks-yt` | `hahn.yt.yandex.net`:80,443 |


## ecstatic Datasets

Нет

## What happens when service is down

В Народной Карте перестанут запускаться валидации и поиск подозрительных правок.
Картографы не смогут проверять датасеты во всех ветках (рабочей, подтвержденной, релизной...)

## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_yt_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_yt_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_yt_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_yt_unstable |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-tasks-yt-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-yt-stable-panel-main) |
| Testing | [maps-core-nmaps-tasks-yt-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-yt-testing-panel-main) |
| Unstable | [maps-core-nmaps-tasks-yt-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-yt-unstable-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro) |
| database | [mapspro_validation](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3aee79ba-6480-4d9d-88d8-020585c701b3;dbname=mapspro_validation) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | grinder/cron | URL/path |
|---|---|---|
| wiki-diffalert-worker | grinder | /var/log/yandex/maps/wiki/diffalert/worker.log* |
| wiki-validation-worker | grinder | /var/log/yandex/maps/wiki/validation/worker.log* |
| wiki-validation-worker-heavy | grinder | /var/log/yandex/maps/wiki/validation/worker-heavy.log* |
| supervisord | - | /var/log/supervisor/* |
| syslog (unfiltered) | - | /var/log/syslog |

## Regression Stress Testing Configurations

Нет


