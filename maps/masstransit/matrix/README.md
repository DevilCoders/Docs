# Masstransit matrix router

Маршрутизатор, строит маршруты на общественном транспорте и пешком, предназначен для тяжелых матричных запросов.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Иван Лапшов](https://staff.yandex-team.ru/lapshov), [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin)  |
| Исходники | [maps/masstransit/matrix](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix) |
| Сервис в ABC | [maps-core-masstransit-matrix](https://abc.yandex-team.ru/services/maps-core-masstransit-matrix/)|
| Проект в CI | [maps-core-masstransit-matrix](https://a.yandex-team.ru/projects/maps-core-masstransit-matrix/ci/actions/launches?dir=maps/masstransit/matrix) |

## Instances

| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_matrix_stable/|
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_matrix_prestable/|
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_matrix_testing/|
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_matrix_datatesting/|
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_matrix_load/|


## API

[README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/masstransit_matrix/README.md#mtmatrix-http-api-2)

## Documentation

* https://wiki.yandex-team.ru/maps/dev/core/masstransit/api/mtmatrix/

## What happens when service is down

У клиентов перестают строиться пешеходные и ОТ-матрицы

## Known clients
| Client | TVM id |
|--------|--------|
| b2bgeo | 2011656 |
| b2bgeo syncsolver | 2024289, 2024291(testing) |
| taxi logistic dispatcher | 2020945 |

## Ecstatic Datasets

The same as [maps/masstransit/router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router)

| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) |
| [yandex-maps-pedestrian-graph-fb](http://ecstatic.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) | [yandex-maps-pedestrian-graph-fb](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) | [yandex-maps-pedestrian-graph-fb](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) |
| [yandex-maps-geodata5](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geodata5/versions) |
| [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

How to restart service
  * Можно по ssh в контейнере дернуть `yacare restart mtmatrix`
  * Либо использовать Instances->State в nanny

Горит мониторинг maps-ecstatic-*
  * Поискать такой случай https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#monitoringchecks
  * Звать на помощь geo-infra


Не переключаются данные в ecstatic:
  * Посмотреть статус и ошибки в http://ecstatic.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions, http://ecstatic.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions (для testing/load использовать тестовый координатор ecstatic-а)
  * Посмотреть лог ecstatic-agent-а /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log
  * Если ошибка во время switch, и она разовая, можно "подтолкнуть" версию ещё раз с помощью `ecstatic reset_errors <dataset>=<version> GROUP`
  * Посмотреть, качаются ли торренты: /var/run/yandex/maps/ecstatic/ymtorrent.status
  * Звать на помощь geo-infra
  * (Advanced) Если не происходит switch, но в ecstatic-agent.log ничего нет:
    * Проверить времена файлов в /var/run/yandex/maps/ecstatic/ - там можно увидеть когда worker успешно запускался и успешно завершался
    * Запустить worker вручную /usr/lib/yandex/maps/ecstatic/worker.sh и посмотреть, на что он ругается.

## Balancers
* Production:
  * Nanny-сервисы l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-matrix_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-matrix_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-matrix_maps_yandex_net_vla/
  * AWACS-балансеры: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-masstransit-matrix.maps.yandex.net/show/

* Testing: общий карточный балансер common.testing.maps.yandex.net
* Datatesting: общий карточный балансер common.datatesting.maps.yandex.net

## Balancers URL
Environment | URL
------------|-
production  | http://core-masstransit-matrix.maps.yandex.net/
testing     | http://core-masstransit-matrix.common.testing.maps.yandex.net/
datatesting | http://core-masstransit-matrix.common.datatesting.maps.yandex.net/

## S3
Результаты асинхронных запросов временно хранятся в s3-mds. Мы используем следующие бакеты:
| Staging | Bucket | max size | graphics |
|---------|--------|----------|----------|
| stable+prestable | matrix-result | 1 Tb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=matrix-result;owner=32827 |
| testing | matrix-result-testing | 100 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=matrix-result-testing;owner=32827 |
| datatesting | matrix-result-datatesting | 50 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=matrix-result-datatesting;owner=32827 |
| unstable | matrix-result-unstable | 50 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=matrix-result-unstable;owner=32827 |

Управление ими осуществляется с помощью [панели Yandex.Cloud](https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/storage)

Для каждого из них должен быть настроен:
  * максимальный размер бакета
  * публичный доступ на чтение объектов
  * удаление старых объектов ("Жизненный цикл" в меню)

Для экономии места кроме штатного удаления объектов старше 1 суток мы также регулярно запускаем sandbox-таску, удаляющую объекты старше 5000 секунд:
  * [планировщик mtmatrix s3 cleanup](https://sandbox.yandex-team.ru/scheduler/82737/tasks?hidden=true&all_tags=false&all_hints=false&limit=20)
  * [планировщик, собирающий бинарь для сборщика мусора](https://sandbox.yandex-team.ru/scheduler/82736/tasks?hidden=true&all_tags=false&all_hints=false&limit=20) - при изменениях в коде s3cleanup нужно дождаться его пересборки, либо запустить ее вручную.

## MDB
Для работы асинхронных запросов необходима распределенная база данных. Мы используем [Managed Service for MongoDB из Yandex.Cloud](https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/managed-mongodb)

Для каждого стейджинга создан свой кластер, как правило, распределенный по нашим 3-м ДЦ:
| Staging | Cluster | Monitoring |
|---------|---------|------------|
| stable+prestable | maps-core-masstransit-matrix-stable | https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/managed-mongodb/cluster/mdb6v6qmudjorud2jg18?section=monitoring |
| testing | maps-core-masstransit-matrix-testing | https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/managed-mongodb/cluster/mdbobg2m2jre0tspucp5?section=monitoring |
| datatesting | maps-core-masstransit-matrix-datatesting | https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/managed-mongodb/cluster/mdbkk50cj40lu1ebkuha?section=monitoring |
| unstable | maps-core-masstransit-matrix-unstable | https://yc.yandex-team.ru/folders/akui9e0hh6bp7sc3qfgl/managed-mongodb/cluster/mdblorih1m1pidhak877?section=monitoring |

Пароли доступа можно найти в секретнице по тэгу [MDB](https://yav.yandex-team.ru/?tags=mdb) (если у вас есть роль "Администратор MDB" или "Руководитель")

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2025067](https://abc.yandex-team.ru/services/maps-core-masstransit-matrix/resources/)
datatesting  | [2025069](https://abc.yandex-team.ru/services/maps-core-masstransit-matrix/resources/)
production   | [2025065](https://abc.yandex-team.ru/services/maps-core-masstransit-matrix/resources/)

## Мониторинги
| Type                         | URL                                                                                                        |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Juggler (all)                | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_*>             |
| Juggler (stable)             | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_stable>        |
| Juggler (prestable)          | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_prestable>     |
| Juggler (testing)            | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_testing>       |
| Juggler (datatesting)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_datatesting>   |
| Juggler (load)               | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_matrix_load>          |

Настройки SEDEM: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix/sedem_config

## Графики
| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-matrix;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-matrix;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-matrix;ctype=datatesting/>      |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-matrix;ctype=load/>             |

SEDEM панели

| Type                         | URL                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-matrix-stable-panel-main/>      |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-matrix-testing-panel-main/>     |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-matrix-datatesting-panel-main/> |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-matrix-load-panel-main/> |
| Ratelimiter                  | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit_matrix-ratelimiter2-panel>      |

## SLA
* [Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_masstransit_matrix)
* [Определение проверки в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_masstransit_matrix.py)

## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Mtmatrix | /var/log/yandex/maps/mtmatrix/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | <https://yql.yandex-team.ru/Operations/YCZzH_MBw4rPSnR0W1Bvbub6TlVczMDDhavVIeVZ8yA=> SELECT * FROM hahn.\`logs/maps-log/1d/2021-02-11\` WHERE vhost = 'core-masstransit-matrix.maps.yandex.net' AND request REGEXP 'matrix' LIMIT 100; |
| YT (detailed logs) | <https://yt.yandex-team.ru/hahn/navigation?filter=maps-mtmatrix-&path=//home/logfeller/logs> |
| Logbroker topics (detailed logs) | <https://lb.yandex-team.ru/logbroker/accounts/maps-mtmatrix> |

## Shootings on test cluster

[Shooter README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix/shooter/README.md)


## Regression Stress Testing Configurations
| Type | URL |
|---|---|
| Lunapark charts | <https://lunapark.yandex-team.ru/regress/MTDEV?service=Mtmatrix> |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/43233/view> |
| Sandbox Task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtmatrixShooting/__init__.py> |


