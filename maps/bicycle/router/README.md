# maps-core-bicycle-router
Велосипедный маршрутизатор, строит велосипедные маршруты.

## General information

| Key | Value |
|---|---|
| Ответственные разработчики | [Иван Лапшов](https://staff.yandex-team.ru/lapshov), [Сергей Кузнецов](https://staff.yandex-team.ru/kuzns), [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin) |
| Исходники | [maps/bicycle/router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router) |
| Сервис в ABC | [maps-core-bicycle-router](https://abc.yandex-team.ru/services/maps-core-bicycle-router/) |
| Проект в CI | [maps-core-bicycle-router](https://a.yandex-team.ru/projects/maps-core-bicycle-router/ci/actions/launches?dir=maps/bicycle/router) |

## Instances

| Environment | URL |
|---|---|
| Сервисы в няне | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_stable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_prestable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_testing/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_datatesting/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_datavalidation/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_datatestingvalidation/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bicycle_router_load/|

## Documentation

* https://wiki.yandex-team.ru/maps/dev/core/masstransit/api/bicyclerouter/
* https://wiki.yandex-team.ru/jandekskarty/projects/catalog/navi/Bicycle-routes/
* https://wiki.yandex-team.ru/AlekseyLobanov/bicycle/routing/

## Known clients

* Bicycle-int
* Mobile-proxy

## Ecstatic Datasets
* http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions
* http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions
* http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-bicycle-graph-fb/versions

## What happens when service is down
На maps.yandex.ru и в МЯК перестанут строиться велосипедные маршруты.

## How to fix common problems

`{{Describe what SRE should do to resuscitate service: how to restart service, change log levels, and fix some known issues}}`

## Balancers URL
Environment | URL
------------|-
production  | http://core-bicycle-router.maps.yandex.net/
datatesting | http://core-bicycle-router.common.datatesting.maps.yandex.net/
testing     | http://core-bicycle-router.common.testing.maps.yandex.net/
datavalidation | http://core-bicycle-router.common.datavalidation.maps.yandex.net/
datatestingvalidation | http://core-bicycle-router.common.datatestingvalidation.maps.yandex.net/


## Балансеры
* Production:
  * Nanny-сервисы l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-router_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-router_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bicycle-router_maps_yandex_net_vla/
  * AWACS-балансеры: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-bicycle-router.maps.yandex.net/show/
  * Мониторинг: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dcore-bicycle-router.maps.yandex.net&statuses=WARN%2CCRIT%2COK

* Testing: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-bicycle-router-testing-slb
* Datatesting: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-bicycle-router-datatesting-slb

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2012606](https://abc.yandex-team.ru/services/maps-core-bicycle-router/resources/)
datatesting  | [2012614](https://abc.yandex-team.ru/services/maps-core-bicycle-router/resources/)
production   | [2012594](https://abc.yandex-team.ru/services/maps-core-bicycle-router/resources/)

## Мониторинги
| Type                         | URL                                                                                                                                                                                                           |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Juggler (all)                | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_*> |
| Juggler (stable)             | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_stable>                                                                                                               |
| Juggler (prestable)          | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_prestable>                                                                                                            |
| Juggler (testing)            | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_testing>                                                                                                              |
| Juggler (datatesting)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_datatesting>                                                                                                          |
| Juggler (datavalidation)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_datavalidation>                                                                                                       |
| Juggler (datatestingvalidation)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bicycle_router_datatestingvalidation>                                                                                                |

Настройки SEDEM: https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router/sedem_config

## Графики
| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=datatesting/>      |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=load/>             |
| Golovan (datavalidation)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=datavalidation/>      |
| Golovan (datatestingvalidation)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-bicycle-router;ctype=datatestingvalidation/>      |

SEDEM панели

| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-stable-panel-main/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-testing-panel-main/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-datatesting-panel-main/>      |
| Golovan (datavalidation)        | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-datavalidation-panel-main/>      |
| Golovan (datatestingvalidation)        | <https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-datatestingvalidation-panel-main/>      |


Quotateka provider dashboards

| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
|  Quotateka (stable)          | <https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_provider_dashboard/abc=maps-core-bicycle-router/>      |
|  Quotateka (testing)         | <https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_testing_provider_dashboard/abc=maps-core-bicycle-router/>      |

## SLA

[График](https://charts.yandex-team.ru/preview/wizard/maps_SLA/maps_core_bicycle_router)
[Определение проверки в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_bicycle_router.py)
[Отчёт на страничке Статистики](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_bicycle_router)

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Bicycle router | /var/log/yandex/maps/bicycle_router/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru/Operations/WtilAkeUGU9WkVRiwADjobwu0jwgoQnzD2CoLFsCChw= SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-04-18] WHERE vhost = 'core-bicycle-router.maps.yandex.net' |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Lunapark charts | https://lunapark.yandex-team.ru/regress/MTDEV?service=Bicycle%20router |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/14431/view> |
| Sandbox Task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsBicycleRouterShooting/__init__.py> |
