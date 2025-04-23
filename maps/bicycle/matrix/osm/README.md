# Bicycle matrix router over OSM

Маршрутизатор для велосипедов и самокатов по данным из OSM, предназначен для тяжелых матричных запросов.


## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Алексей Буглаков](https://staff.yandex-team.ru/avbuglakov), [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin) |
| Отвественные SRE | Алексей Буглаков (avbuglakov@yandex-team.ru) <br/> Андрей Козлов (pedeathtrian@yandex-team.ru) <br/> Антон Овчинкин (ovchinkin@yandex-team.ru) <br/> Иван Лапшов (lapshov@yandex-team.ru) <br/> Михаил Прохоров (aphanasiy@yandex-team.ru) <br/> Никита Харитонов (redoak@yandex-team.ru) <br/> Сергей Кузнецов (kuzns@yandex-team.ru) |
| Исходники | [maps/bicycle/matrix](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix) |
| Сервис в ABC | [maps-core-bicycle-matrix-over-osm](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix-over-osm/)|
| Проект в CI | [maps-core-bicycle-matrix-over-osm](https://a.yandex-team.ru/projects/maps-core-bicycle-matrix-over-osm/ci/actions/launches?dir=maps/bicycle/matrix/osm) |


## Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
|-------------|---------------|----------------|-------------------|
| Datatesting | [maps_core_bicycle_matrix_over_osm_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_over_osm_datatesting/) | [core-bicycle-matrix-over-osm.datatesting](https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-datatesting-panel-main/) | [maps_core_bicycle_matrix_over_osm_datatesting](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_over_osm_datatesting) |
| Load | [maps_core_bicycle_matrix_over_osm_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_over_osm_load/) | [core-bicycle-matrix-over-osm.load](https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-load-panel-main/) | [maps_core_bicycle_matrix_over_osm_load](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_over_osm_load) |
| Prestable | [maps_core_bicycle_matrix_over_osm_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_over_osm_prestable/) | [core-bicycle-matrix-over-osm.prestable](https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-prestable-panel-main/) | [maps_core_bicycle_matrix_over_osm_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_over_osm_prestable) |
| Stable | [maps_core_bicycle_matrix_over_osm_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_over_osm_stable/) | [core-bicycle-matrix-over-osm.stable](https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-stable-panel-main/) | [maps_core_bicycle_matrix_over_osm_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_over_osm_stable) |
| Testing | [maps_core_bicycle_matrix_over_osm_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_matrix_over_osm_testing/) | [core-bicycle-matrix-over-osm.testing](https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-testing-panel-main/) | [maps_core_bicycle_matrix_over_osm_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_matrix_over_osm_testing) |

[Monitorings all (tag=a_prj_maps-core-bicycle-matrix-over-osm)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-bicycle-matrix-over-osm)

## Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
|---------|------|----------------|----------------|-------------------------|
| Datatesting | common_default | [core-bicycle-matrix-over-osm.common.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list?filter=%7B%22idRegexp%22:%22core-bicycle-matrix-over-osm.common.datatesting.maps.yandex.net%22%7D) | [core-bicycle-matrix-over-osm.common.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatesting.maps.yandex.net;prj=common.datatesting.maps.yandex.net;signal=core-bicycle-matrix-over-osm_common_datatesting_maps_yandex_net;) | [rtc_balancer_common_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_sas) <br/> [rtc_balancer_common_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_man) <br/> [rtc_balancer_common_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_vla) |
| Stable | default | [core-bicycle-matrix-over-osm.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-bicycle-matrix-over-osm.maps.yandex.net/) | [core-bicycle-matrix-over-osm.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=;fqdn=core-bicycle-matrix-over-osm.maps.yandex.net;prj=core-bicycle-matrix-over-osm;signal=service_total;) | [rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_man) <br/> [rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_sas) <br/> [rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-matrix-over-osm_maps_yandex_net_vla) |
| Testing | common_default | [core-bicycle-matrix-over-osm.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter=%7B%22idRegexp%22:%22core-bicycle-matrix-over-osm.common.testing.maps.yandex.net%22%7D) | [core-bicycle-matrix-over-osm.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-bicycle-matrix-over-osm_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br/> [rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br/> [rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |


## Firewall Macroses

| staging | URL |
|---------|-----|
| Datatesting | [_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_DATATESTING_RTC_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_DATATESTING_RTC_NETS_) |
| Load | [_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_LOAD_RTC_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_LOAD_RTC_NETS_) |
| Stable | [_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_STABLE_RTC_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_STABLE_RTC_NETS_) |
| Testing | [_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_TESTING_RTC_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BICYCLE_MATRIX_OVER_OSM_TESTING_RTC_NETS_) |


## Ecstatic Datasets

| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-bicycle-graph-over-osm-fb](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-bicycle-graph-over-osm-fb/versions) | [yandex-maps-bicycle-graph-over-osm-fb](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-bicycle-graph-over-osm-fb/versions) | [yandex-maps-bicycle-graph-over-osm-fb](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-bicycle-graph-over-osm-fb/versions) |


## API

[README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/README.md)


## What happens when service is down

У клиентов перестают строиться велосипедные/самокатные матрицы


## Known clients

FIXME


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

How to restart service
  * Можно по ssh в контейнере дернуть `yacare restart mtmatrix`
  * Либо использовать Instances->State в nanny

Горит мониторинг maps-ecstatic-*
  * Поискать такой случай https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#monitoringchecks
  * Звать на помощь geo-infra


Не переключаются данные в ecstatic:
  * Посмотреть статус и ошибки в http://ecstatic.maps.yandex.net/pkg/yandex-maps-bicycle-graph-over-osm-fb/versions (для testing/load использовать тестовый координатор ecstatic-а)
  * Посмотреть лог ecstatic-agent-а /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log
  * Если ошибка во время switch, и она разовая, можно "подтолкнуть" версию ещё раз с помощью `ecstatic reset_errors <dataset>=<version> GROUP`
  * Посмотреть, качаются ли торренты: /var/run/yandex/maps/ecstatic/ymtorrent.status
  * Звать на помощь geo-infra
  * (Advanced) Если не происходит switch, но в ecstatic-agent.log ничего нет:
    * Проверить времена файлов в /var/run/yandex/maps/ecstatic/ - там можно увидеть когда worker успешно запускался и успешно завершался
    * Запустить worker вручную /usr/lib/yandex/maps/ecstatic/worker.sh и посмотреть, на что он ругается.



## S3
Результаты асинхронных запросов временно хранятся в s3-mds. Мы используем следующие бакеты:
| Staging          | Bucket                            | max size | graphics                                                                                                           |
|------------------|-----------------------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| stable+prestable | bicycle-matrix-over-osm-result             | 400 Gb   | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-over-osm-result;owner=37277             |
| testing          | bicycle-matrix-over-osm-result-testing     | 100 Gb   | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-over-osm-result-testing;owner=37277     |
| datatesting      | bicycle-matrix-over-osm-result-datatesting | 50 Gb    | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-over-osm-result-datatesting;owner=37277 |
| unstable         | bicycle-matrix-over-osm-result-unstable    | 50 Gb    | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=bicycle-matrix-over-osm-result-unstable;owner=37277    |

Управление ими осуществляется с помощью [панели Yandex.Cloud](https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/storage)

Для каждого из них должен быть настроен:
  * максимальный размер бакета
  * публичный доступ на чтение объектов
  * удаление старых объектов ("Жизненный цикл" в меню)

Для экономии места кроме штатного удаления объектов старше 1 суток мы также регулярно запускаем sandbox-таску, удаляющую объекты старше 5000 секунд:
  * [планировщик mtmatrix s3 cleanup](https://sandbox.yandex-team.ru/scheduler/82737/tasks?hidden=true&all_tags=false&all_hints=false&limit=20)
  * [планировщик, собирающий бинарь для сборщика мусора](https://sandbox.yandex-team.ru/scheduler/82736/tasks?hidden=true&all_tags=false&all_hints=false&limit=20) - при изменениях в коде s3cleanup нужно дождаться его пересборки, либо запустить ее вручную.


## MDB
Для работы асинхронных запросов необходима распределенная база данных. Мы используем [Managed Service for MongoDB из Yandex.Cloud](https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/managed-mongodb)

Для каждого стейджинга создан свой кластер, как правило, распределенный по нашим 3-м ДЦ:
| Staging          | Cluster                                       | Monitoring                                                                                                             |
|------------------|-----------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| stable+prestable | maps-core-bicycle-matrix-over-osm-stable      | https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/managed-mongodb/cluster/mdb1c5ajkbg4tdger0eu?section=monitoring |
| testing          | maps-core-bicycle-matrix-over-osm-testing     | https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/managed-mongodb/cluster/mdbfiel7n0gcl6mfl76v?section=monitoring |
| datatesting      | maps-core-bicycle-matrix-over-osm-datatesting | https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/managed-mongodb/cluster/mdb3e628ru16glsmei16?section=monitoring |
| unstable         | maps-core-bicycle-matrix-over-osm-unstable    | https://yc.yandex-team.ru/folders/aku3qd38lvf7m7d2dpq6/managed-mongodb/cluster/mdbl2o22mj5ghcd708up?section=monitoring |

Пароли доступа можно найти в секретнице по тэгу [MDB](https://yav.yandex-team.ru/?search=mdb.password.bicycle-matrix-over-osm&tags=mdb) (если у вас есть роль "Администратор MDB" или "Руководитель")


## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2032768](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix-over-osm/resources/)
datatesting  | [2032770](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix-over-osm/resources/)
production   | [2032772](https://abc.yandex-team.ru/services/maps-core-bicycle-matrix-over-osm/resources/)


## Настройки SEDEM
https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix/osm/sedem_config

## Графики
| Type                         | URL                                                                                                                                         |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix-over-osm;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix-over-osm;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix-over-osm;ctype=datatesting/>      |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-matrix-over-osm;ctype=load/>             |

SEDEM панели

| Type                         | URL                                                                                                    |
|------------------------------|--------------------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-stable-panel-main/>      |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-testing-panel-main/>     |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-datatesting-panel-main/> |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-matrix-over-osm-load-panel-main/>        |
| Ratelimiter                  | <https://yasm.yandex-team.ru/template/panel/maps_core_bicycle_matrix-over-osm-ratelimiter2-panel>      |

## SLA

FIXME: Включим, когда пойдет ежедневный поток запросов

## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name                             | URL/path                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nginx                            | /var/log/nginx/*                                                                                                                                                                                                                                                                                                                                                |
| Yacare                           | /var/log/yandex/maps/yacare/*                                                                                                                                                                                                                                                                                                                                   |
| Bicycle matrix over OSM          | /var/log/yandex/maps/bicycle_matrix/*                                                                                                                                                                                                                                                                                                                           |
| Ecstatic                         | /var/log/yandex/maps/ecstatic-agent/*                                                                                                                                                                                                                                                                                                                           |
| Supervisord                      | /var/log/supervisor/*                                                                                                                                                                                                                                                                                                                                           |
| Syslog (unfiltered)              | /var/log/syslog                                                                                                                                                                                                                                                                                                                                                 |
| YT                               | <https://yql.yandex-team.ru/Operations/YgZ5ipfFt9CzkJPsyKlaIPLotTpMH2jnvkSxdtYQV-Q=> SELECT * FROM hahn.\`logs/maps-log/1d/2022-02-10\` WHERE vhost = 'core-bicycle-matrix-over-osm.maps.yandex.net' AND request REGEXP 'matrix' LIMIT 100; |
| YT (detailed logs)               | https://yt.yandex-team.ru/hahn/navigation?filter=maps-bicycle-matrix-over-osm&path=//home/logfeller/logs                                                                                                                                                                                                                                                        |
| Logbroker topics (detailed logs) | https://lb.yandex-team.ru/logbroker/accounts/maps-bicycle-matrix-over-osm                                                                                                                                                                                                                                                                                       |

## Shootings on test cluster

[Shooter README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix/shooter/README.md)


## Regression Stress Testing Configurations

| Type              | URL                                                                                                             |
|-------------------|-----------------------------------------------------------------------------------------------------------------|
| Lunapark charts   | <https://lunapark.yandex-team.ru/regress/MTDEV?service=Bicycle%20matrix%20over%20OSM>           |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/703532/view>                                                          |
| Sandbox Task      | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsBicycleMatrixShooting/__init__.py> |


