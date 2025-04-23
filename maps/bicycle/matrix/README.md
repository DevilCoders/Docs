# Bicycle matrix router

Маршрутизатор, строит велосипедные и самокатные маршруты, предназначен для тяжелых матричных запросов.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Иван Лапшов](https://staff.yandex-team.ru/lapshov), [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin) |
| Исходники | [maps/bicycle/matrix](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix) |
| Сервис в ABC | [maps-core-bicycle-matrix](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix/)|
| Проект в CI | [maps-core-bicycle-matrix](https://a.yandex-team.ru/projects/maps-core-bicycle-matrix/ci/actions/launches?dir=maps/bicycle/matrix) |

## Instances

| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_stable/|
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_prestable/|
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_testing/|
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_datatesting/|
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_load/|


## API

[README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/README.md)


## What happens when service is down

У клиентов перестают строиться велосипедные/самокатные  матрицы

## Known clients

FIXME

## Ecstatic Datasets

The same as [maps/bicycle/router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router)

| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-bicycle-graph-fb](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions) | [yandex-maps-bicycle-graph-fb](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions) | [yandex-maps-bicycle-graph-fb](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions) |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

How to restart service
  * Можно по ssh в контейнере дернуть `yacare restart mtmatrix`
  * Либо использовать Instances->State в nanny

Горит мониторинг maps-ecstatic-*
  * Поискать такой случай https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#monitoringchecks
  * Звать на помощь geo-infra


Не переключаются данные в ecstatic:
  * Посмотреть статус и ошибки в http://ecstatic.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions (для testing/load использовать тестовый координатор ecstatic-а)
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
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix_maps_yandex_net_vla/
  * AWACS-балансеры: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-bicycle-matrix.maps.yandex.net/show/

* Testing: общий карточный балансер common.testing.maps.yandex.net
* Datatesting: общий карточный балансер common.datatesting.maps.yandex.net

## Balancers URL
Environment | URL
------------|-
production  | http://core-bicycle-matrix.maps.yandex.net/
testing     | http://core-bicycle-matrix.common.testing.maps.yandex.net/
datatesting | http://core-bicycle-matrix.common.datatesting.maps.yandex.net/

## S3
Результаты асинхронных запросов временно хранятся в s3-mds. Мы используем следующие бакеты:
| Staging | Bucket | max size | graphics |
|---------|--------|----------|----------|
| stable+prestable | bicycle-matrix-result | 400 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-result;owner=34698 |
| testing | bicycle-matrix-result-testing | 100 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-result-testing;owner=34698 |
| datatesting | bicycle-matrix-result-datatesting | 50 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-result-datatesting;owner=34698 |
| unstable | bicycle-matrix-result-unstable | 50 Gb | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-result-unstable;owner=34698 |

Управление ими осуществляется с помощью [панели Yandex.Cloud](https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/storage)

Для каждого из них должен быть настроен:
  * максимальный размер бакета
  * публичный доступ на чтение объектов
  * удаление старых объектов ("Жизненный цикл" в меню)

Для экономии места кроме штатного удаления объектов старше 1 суток мы также регулярно запускаем sandbox-таску, удаляющую объекты старше 5000 секунд:
  * [планировщик mtmatrix s3 cleanup](https://sandbox.yandex-team.ru/scheduler/82737/tasks?hidden=true&all_tags=false&all_hints=false&limit=20)
  * [планировщик, собирающий бинарь для сборщика мусора](https://sandbox.yandex-team.ru/scheduler/82736/tasks?hidden=true&all_tags=false&all_hints=false&limit=20) - при изменениях в коде s3cleanup нужно дождаться его пересборки, либо запустить ее вручную.

## MDB
Для работы асинхронных запросов необходима распределенная база данных. Мы используем [Managed Service for MongoDB из Yandex.Cloud](https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/managed-mongodb)

Для каждого стейджинга создан свой кластер, как правило, распределенный по нашим 3-м ДЦ:
| Staging | Cluster | Monitoring |
|---------|---------|------------|
| stable+prestable | maps-core-bicycle-matrix-stable | https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/managed-mongodb/cluster/mdb67g18sgtm5moguvkd?section=monitoring |
| testing | maps-core-bicycle-matrix-testing | https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/managed-mongodb/cluster/mdbdl76o1as5ck3j0rkr?section=monitoring |
| datatesting | maps-core-bicycle-matrix-datatesting | https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/managed-mongodb/cluster/mdbn2p4r2chddua1m9sf?section=monitoring |
| unstable | maps-core-bicycle-matrix-unstable | https://yc.yandex-team.ru/folders/akutmjortf8o626n9n9d/managed-mongodb/cluster/mdbu5vpocm9uvmsas1b1?section=monitoring |

Пароли доступа можно найти в секретнице по тэгу [MDB](https://yav.yandex-team.ru/?tags=mdb) (если у вас есть роль "Администратор MDB" или "Руководитель")

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2028431](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix/resources/)
datatesting  | [2028433](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix/resources/)
production   | [2028435](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix/resources/)

## Мониторинги
| Type                         | URL                                                                                                        |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Juggler (all)                | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_*>             |
| Juggler (stable)             | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_stable>        |
| Juggler (prestable)          | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_prestable>     |
| Juggler (testing)            | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_testing>       |
| Juggler (datatesting)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_datatesting>   |
| Juggler (load)               | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_load>          |

Настройки SEDEM: https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix/sedem_config

## Графики
| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix;ctype=datatesting/>      |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix;ctype=load/>             |

SEDEM панели

| Type                         | URL                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-stable-panel-main/>      |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-testing-panel-main/>     |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-datatesting-panel-main/> |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-load-panel-main/> |
| Ratelimiter                  | <https://yasm.yandex-team.ru/template/panel/maps_core_bicycle_matrix-ratelimiter2-panel>      |

## SLA

FIXME: Включим, когда пойдет ежедневный поток запросов

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
| YT | <https://yql.yandex-team.ru/Operations/YOV1-wuEI5Ok9BZzfWchgYpqbAx56O5_RtTJedP12TI=> SELECT * FROM hahn.\`logs/maps-log/1d/2021-07-06\` WHERE vhost = 'core-bicycle-matrix.maps.yandex.net' AND request REGEXP 'matrix' LIMIT 100; |
| YT (detailed logs) | <https://yt.yandex-team.ru/hahn/navigation?filter=maps-bicycle-matrix&path=//home/logfeller/logs |
| Logbroker topics (detailed logs) | <https://lb.yandex-team.ru/logbroker/accounts/maps-bicycle-matrix> |

## Shootings on test cluster

[Shooter README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix/shooter/README.md)


## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Lunapark charts | <https://lunapark.yandex-team.ru/regress/MTDEV?service=Bicycle%20matrix> |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/411011/view> |
| Sandbox Task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsBicycleMatrixShooting/__init__.py> |


