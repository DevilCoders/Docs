# maps-core-masstransit-router
Пешеходный и ОТ маршрутизатор, строит пешеходные маршруты и маршруты на общественном транспорте.

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | [Иван Лапшов](https://staff.yandex-team.ru/lapshov), [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin), [Алексей Буглаков](https://staff.yandex-team.ru/avbuglakov) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router |
| Сервис в ABC | [maps-core-masstransit-router](https://abc.yandex-team.ru/services/maps-core-masstransit-router/) |
| Проект в CI | [maps-core-masstransit-router](https://a.yandex-team.ru/projects/maps-core-masstransit-router/ci/actions/launches?dir=maps/masstransit/router) |

## Instances

| Environment | URL |
|---|---|
| Сервисы в няне | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_stable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_prestable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_testing/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_datatesting/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_load/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_datavalidation/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_router_datatestingvalidation/|

## Documentation

* https://wiki.yandex-team.ru/maps/dev/core/masstransit/api/mtrouter/
* https://wiki.yandex-team.ru/maps/dev/core/masstransit/

## Known clients

* API и БЯК
* Mobile-proxy
* Работа
* Недвижимость
* Райдтех
* Бэкенд Алисы (origin=assistant_bass)

## Ecstatic Datasets
| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) |
| [yandex-maps-pedestrian-graph-fb](http://ecstatic.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) | [yandex-maps-pedestrian-graph-fb](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) | [yandex-maps-pedestrian-graph-fb](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) |
| [yandex-maps-geodata5](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geodata5/versions) |
| [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |


## What happens when service is down
На maps.yandex.ru, в МЯК и Транспорте перестанут строиться пешеходные и ОТ маршруты. В сниппете masstransit/2.x пропадут честные пешеходные расстояния и будут отображаться расстояния по прямой.

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/maps/dev/core/Instrukcija-po-sozdaniju-servisov-v-RTC/whatcangowronginrtc/)

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

## Балансеры
* Production:
  * Nanny-сервисы l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-router_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-router_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-router_maps_yandex_net_vla/
  * AWACS-балансеры: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-masstransit-router.maps.yandex.net/show/

* Testing: общий карточный балансер common.testing.maps.yandex.net
* Datatesting: общий карточный балансер common.datatesting.maps.yandex.net
* Datavalidation: общий карточный балансер common.datavalidation.maps.yandex.net
* Datatestingvalidation: общий карточный балансер common.datatestingvalidation.maps.yandex.net

## Balancers URL
Environment    | URL
---------------|-
testing        | http://core-masstransit-router.common.testing.maps.yandex.net/
production     | http://core-masstransit-router.maps.yandex.net/
datatesting    | http://core-masstransit-router.common.datatesting.maps.yandex.net/
datavalidation | http://core-masstransit-router.common.datavalidation.maps.yandex.net/
datatestingvalidation | http://core-masstransit-router.common.datatestingvalidation.maps.yandex.net/

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2012632](https://abc.yandex-team.ru/services/maps-core-masstransit-router/resources/)
datatesting  | [2012632](https://abc.yandex-team.ru/services/maps-core-masstransit-router/resources/)
production   | [2012630](https://abc.yandex-team.ru/services/maps-core-masstransit-router/resources/)

## Мониторинги
| Type                         | URL                                                                                                                                                                                                           |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Juggler (all)                | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_*> |
| Juggler (stable)             | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_stable>                                                                                                               |
| Juggler (prestable)          | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_prestable>                                                                                                            |
| Juggler (testing)            | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_testing>                                                                                                              |
| Juggler (datatesting)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_datatesting>                                                                                                          |
| Juggler (datavalidation)     | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_datavalidation>                                                                                                          |
| Juggler (datatestingvalidation)     | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_router_datatestingvalidation>

Настройки SEDEM: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router/sedem_config

## Графики
| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=datatesting/>      |
| Golovan (load)               | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=load/>             |
| Golovan (datavalidation)     | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=datavalidation/>   |
| Golovan (datatestingvalidation)     | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-router;ctype=datatestingvalidation/>   |

SEDEM панели

| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-stable-panel-main/> |
| Golovan (prestable-only)     | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-prestable-panel-main/>  |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-testing-panel-main/>          |
| Golovan (load)            | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-load-panel-main/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-datatesting-panel-main/>      |
| Golovan (datavalidation)     | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-datavalidation-panel-main/>   |
| Golovan (datatestingvalidation)     | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-datatestingvalidation-panel-main/>   |

Quotateka provider dashboards

| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Quotateka  (stable)          | https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_provider_dashboard/abc=maps-core-masstransit-router         |
| Quotateka  (testing)         | https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_testing_provider_dashboard/abc=maps-core-masstransit-router/        |

## SLA
* [Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_masstransit_router)
* [Определение проверки в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_masstransit_router.py)


## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Mtrouter | /var/log/yandex/maps/mtroute/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru/Operations/XCyTw2im9ce3iqM8JMvalrdTZgIB6M6ABkLHzkRcOdc= SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-12-31] WHERE vhost = 'mt-router.maps.yandex.net' |
| YT (detailed logs) | <https://yt.yandex-team.ru/hahn/navigation?filter=maps-mtroute-&path=//home/logfeller/logs> |
| Logbroker topics (detailed logs) | <https://lb.yandex-team.ru/logbroker/accounts/maps-mtroute> |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Lunapark charts | <https://lunapark.yandex-team.ru/regress/MTDEV?service=Mtrouter> |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/14163/view> |
| Sandbox Task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtrouterShooting/__init__.py> |

## Quality regression testing

| Type | URL |
|---|---|
| Sandbox task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtrouterQualityRegression> |
| Results chart | <https://datalens.yandex-team.ru/g4ib8ofl06psc-mtrouter-regression-dashboard>
