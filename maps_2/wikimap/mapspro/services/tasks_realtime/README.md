# wiki-tasks-realtime

Фоновые задачи Народной Карты

## General information

| Key                                  | Value                                                                                                                                |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Кому звонить, если ничего не понятно | Евгений Гагауз ( gagauzev@yandex-team.ru ) Сергей Ливерко ( mr-spock@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники                            | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_realtime                                              |
| Сервис в ABC                         | https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-realtime/                                                                  |
| Проект в CI | [maps-core-nmaps-tasks-realtime](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks-realtime/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks_realtime) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_tasks_realtime/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_realtime_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_realtime_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_realtime_unstable/)

## Documentation

Кроновские задания и фоновые процессы Народной Карты


## Known clients

[puncher](https://puncher.yandex-team.ru/?source=_MAPS_CORE_NMAPS_TASKS_REALTIME_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

| Source                | Destination                               |
|-----------------------|-------------------------------------------|
| `wiki-tasks-realtime` | `_PGAASINTERNALNETS_`:6432                |
| `wiki-tasks-realtime` | `core-nmaps-editor.maps.yandex.net`:80    |
| `wiki-tasks-realtime` | `core-nmaps-tasks.maps.yandex.net`:80     |
| `wiki-tasks-realtime` | `core-garden-server.maps.yandex.net`:80   |
| `wiki-tasks-realtime` | `st-api.yandex-team.ru`:443               |
| `wiki-tasks-realtime` | `tanker.stable.qloud-b.yandex.net`:80,443 |
| `wiki-tasks-realtime` | `upload.stat.yandex-team.ru`:80,443       |
| `wiki-tasks-realtime` | `storage-int.mds.yandex.net`:80,443,1111  |
| `wiki-tasks-realtime` | `hahn.yt.yandex.net`:80                   |


## ecstatic Datasets

Нет


## What happens when service is down

В Народной Карте перестанут обрабатываться фоновые задачи (подтверждаться и синхронизироваться правки, обрабатываться статистика и прочее)

## Как проверить, что сервис работает

https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_realtime_stable

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

Нет

## Мониторинги

| Type                  | URL                                                                                  |
|-----------------------|--------------------------------------------------------------------------------------|
| Juggler (Production)  | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_realtime_stable   |
| Juggler (Testing)     | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_realtime_testing  |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_tasks_realtime_unstable |

| Проверка | Ответственные | Описание |
|----------|---------------|----------|
| wiki-acl-permissions-synchronizer-status | mr-spock@ , euclid@ | Удаление расширенных прав у пользователей Народной карты при увольнении |
| wiki-contour-denormalizer-queue | ponomarev@ , chikunov@ | Размер очереди коммитов, необходимых для расчета геометрии контурных объектов. Как правило, растет из-за открытых транзакций в core-базе, блокирующих новых поток коммитов к pubsub-воркерам |
| wiki-export-deleting-datasets | ponomarev@ , chikunov@ | Удаление результатов устаревших экспортов из MDS |
| wiki-mrc-pedestrian-regions-logger-queue-size | gagauzev@ | Размер очереди логирования зон контроля заданий пешеходам в YT |
| wiki-mrc-pedestrian-tasks-queue | miplot@ | Размер очереди необработанных коммитов зон обхода пешеходами (mrc_pedestrian_region). Очередь может расти из-за повторяющейся ошибки при обработке какой-то зоны, содержащей невалидные данные |
| wiki-publication-check-worker-status | ponomarev@ , likynushka@ , gradksov | Обработка релизных веток, опубликованных в Огороде. Обработка опубликованных коммитов, нотификация в social |
| wiki-release-metrics-apply-shadow-attributes | ponomarev@ , chikunov@ | Задача применения теневых атрибутов к новой релизной ветке. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-release-metrics-create-stable | ponomarev@ , chikunov@ | Задача создания релизной ветки. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-release-metrics-diffalert | ponomarev@ , chikunov@ | Задача создания релизной ветки. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-release-metrics-export | ponomarev@ , chikunov@ | Задача создания релизной ветки. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-release-metrics-prepare-stable-branch | ponomarev@ , chikunov@ | Задача подготовки релизной ветки. Может сломаться из-за проблем с базой или из-за сломанных дочерних задач, алерты по времени выполнения. |
| wiki-release-metrics-validation-export | ponomarev@ , chikunov@ | Задача создания релизной ветки. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-release-metrics-validation-full | ponomarev@ , chikunov@ | Задача создания релизной ветки. Может сломаться из-за проблем с базой, алерты по времени выполнения. |
| wiki-revision-meta-approved-queue-size | ponomarev@ , chikunov@ | Размер очереди для апрува коммитов (draft->approved). Может расти если апрувед-ветка не в рабочем состоянии |
| wiki-revision-meta-bboxes-queue-size | ponomarev@ , chikunov@ | Размер очереди расчета bounding box объектов, может расти при сложных импортах данных (много объектов нужно подписать) |
| wiki-revision-meta-labels-queue-size | ponomarev@ , chikunov@ | Размер очереди синхронизации подписей в appoved-ветке. Может расти при сложных импортах данных (много объектов нужно подписать) |
| wiki-revision-meta-preapproved-queue-size | kgolenkova@ , nfilippova@ , abulich , klimareva , ponomarev , chikunov | Размер preaproved-очереди правок. Может расти из-за блокирующих неразобранных правок |
| wiki-user-edits-metrics-consolidated-deployment-time | gagauzev@ , likynushka@ | Обработка правок пользователей |
| wiki-user-edits-metrics-deployment-sla | gagauzev@ , likynushka@ | Обработка правок пользователей |
| wiki-user-edits-metrics-user-edits-processing | gagauzev@ , likynushka@ | Обработка правок пользователей |


## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging  | Golovan panel URL                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Stable   | [maps-core-nmaps-tasks-realtime-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-realtime-stable-panel-main)            |
| Testing  | [maps-core-nmaps-tasks-realtime-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-realtime-testing-panel-main)          |
| Unstable | [maps-core-nmaps-tasks-realtime-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-realtime-unstable-panel-main)        |
| database | [mapspro_core](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg3hms1oasjh7jtiki;dbname=mapspro)                                  |
| database | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social)                         |
| database | [mapspro_view_trunk](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbhqds4cpsr293br2t3;dbname=mapspro_view_trunk)                 |
| database | [mapspro_view_trunk_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbsj61vh1ob68181o6v;dbname=mapspro_view_trunk_labels)   |
| database | [mapspro_view_stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbe9n7jsv7p2rih4na2;dbname=mapspro_view_stable)               |
| database | [mapspro_view_stable_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb4cb8nj54at9gqh3jf;dbname=mapspro_view_stable_labels) |
| database | [mapspro_validation](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3aee79ba-6480-4d9d-88d8-020585c701b3;dbname=mapspro_validation) |
| all      | [release_metrics](https://datalens.yandex-team.ru/5wcyhpuopo6wy-reliznye-metriki) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name                                    | daemon/cron/tool | URL/path                                                          |
|-----------------------------------------|------------------|-------------------------------------------------------------------|
| supervisord                             | -                | /var/log/supervisor/*                                             |
| syslog (unfiltered)                     | -                | /var/log/syslog                                                   |
| wiki-acl-clusters-updater               | daemon           | /var/log/yandex/maps/wiki/acl/cluster-updater.log*                |
| wiki-acl-permissions-synchronizer       | cron             | /var/log/yandex/maps/wiki/acl-permissions-synchronizer/*          |
| wiki-acl-roles-dumper                   | cron             | /var/log/yandex/maps/wiki/acl-roles-dumper/*                      |
| wiki-approver                           | daemon, cron(4)  | /var/log/yandex/maps/wiki/approver/*                              |
| wiki-contour-denormalizer               | daemon(pubsub)   | /var/log/yandex/maps/wiki/contour-denormalizer/*                  |
| wiki-editor-tool                        | tool             | /usr/lib/yandex/maps/wiki/bin/wiki-editor-tool --help             |
| wiki-edits-logger                       | daemon(pubsub)   | /var/log/yandex/maps/wiki/edits-logger/*                          |
| wiki-export-cleaner                     | cron             | /var/log/yandex/maps/wiki/export/*                                |
| wiki-mrc-pedestrian-regions-logger      | daemon(pubsub)   | /var/log/yandex/maps/wiki/mrc-pedestrian-regions-logger/*         |
| wiki-mrc-pedestrian-tasks-generator     | daemon(pubsub)   | /var/log/yandex/maps/wiki/mrc-pedestrian-tasks-generator/*        |
| wiki-outsource-regions-worker           | daemon(pubsub)   | /var/log/yandex/maps/wiki/outsource-regions/*                     |
| wiki-outsourcer-edits-worker            | daemon(pubsub)   | /var/log/yandex/maps/wiki/outsourcer-edits/*                      |
| wiki-publication-check-worker           | cron             | /var/log/yandex/maps/wiki/publication-check/*                     |
| wiki-release-metrics                    | cron             | /var/log/yandex/maps/wiki/release-metrics/*                       |
| wiki-skills-updater (disabled)          | cron             | /var/log/yandex/maps/wiki/skills-updater/*                        |
| wiki-stat-outsource-regions-dump-worker | cron             | /var/log/yandex/maps/wiki/stat/outsource-regions-dump-worker.log* |
| wiki-stat-users-dump-worker             | cron             | /var/log/yandex/maps/wiki/stat/users-dump-worker.log*             |
| wiki-user-edits-metrics                 | cron             | /var/log/yandex/maps/wiki/user_edits_metrics/*                    |
| wiki-validation-cleaner                 | cron             | /var/log/yandex/maps/wiki/validation/*                            |

## Regression Stress Testing Configurations

Нет
