# Core Driving Router Over Osm

The service allows to find the shortest path between two or more sequential points for cars, taxi and trucks. The service is intented to use with [compact graph](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/road_graph) built based on OSM data.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Константин Колганов (kmkolganov@yandex-team.ru) <br> Константин Ша́льнев (kshalnev@yandex-team.ru) |
| Отвественные SRE | Константин Колганов (kmkolganov@yandex-team.ru) |
| Исходники | [maps/routing/router/osm](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/osm) |
| Сервис в ABC | [maps-core-driving-router-over-osm](https://abc.yandex-team.ru/services/maps-core-driving-router-over-osm/)|
| Проект в CI | [maps-core-driving-router-over-osm](https://a.yandex-team.ru/projects/maps-core-driving-router-over-osm/ci/actions/launches?dir=maps/routing/router/osm) |
| API | https://wiki.yandex-team.ru/maps/dev/core/routing/software/router/newrouterapi/ |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Datatesting | [maps_core_driving_router_over_osm_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_datatesting/) | [ core-driving-router-over-osm.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-datatesting-panel-main/) | [ maps_core_driving_router_over_osm_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_datatesting) |
| Datatestingvalidation | [maps_core_driving_router_over_osm_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_datatestingvalidation/) | [ core-driving-router-over-osm.datatestingvalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-datatestingvalidation-panel-main/) | [ maps_core_driving_router_over_osm_datatestingvalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_datatestingvalidation) |
| Datavalidation | [maps_core_driving_router_over_osm_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_datavalidation/) | [ core-driving-router-over-osm.datavalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-datavalidation-panel-main/) | [ maps_core_driving_router_over_osm_datavalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_datavalidation) |
| Load | [maps_core_driving_router_over_osm_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_load/) | [ core-driving-router-over-osm.load ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-load-panel-main/) | [ maps_core_driving_router_over_osm_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_load) |
| Prestable | [maps_core_driving_router_over_osm_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_prestable/) | [ core-driving-router-over-osm.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-prestable-panel-main/) | [ maps_core_driving_router_over_osm_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_prestable) |
| Stable | [maps_core_driving_router_over_osm_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_stable/) | [ core-driving-router-over-osm.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-stable-panel-main/) | [ maps_core_driving_router_over_osm_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_stable) |
| Testing | [maps_core_driving_router_over_osm_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_over_osm_testing/) | [ core-driving-router-over-osm.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-over-osm-testing-panel-main/) | [ maps_core_driving_router_over_osm_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_over_osm_testing) |

[Monitorings all (tag=a_prj_maps-core-driving-router-over-osm)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-driving-router-over-osm)

### Quotateka

* [Dashboard (stable)](https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_provider_dashboard/abc=maps-core-driving-router-over-osm)
* [Dashboard (testing)](https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_testing_provider_dashboard/abc=maps-core-driving-router-over-osm)
* [Configuration in Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/quotateka/core-driving-router-over-osm)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Datatesting | common_default | [core-driving-router-over-osm.common.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-driving-router-over-osm.common.datatesting.maps.yandex.net"}) | [core-driving-router-over-osm.common.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatesting.maps.yandex.net;prj=common.datatesting.maps.yandex.net;signal=core-driving-router-over-osm_common_datatesting_maps_yandex_net;) | [rtc_balancer_common_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_sas) <br>[rtc_balancer_common_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_man) <br>[rtc_balancer_common_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_vla) |
| Datatestingvalidation | common_default | [core-driving-router-over-osm.common.datatestingvalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatestingvalidation.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-driving-router-over-osm.common.datatestingvalidation.maps.yandex.net"}) | [core-driving-router-over-osm.common.datatestingvalidation.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatestingvalidation.maps.yandex.net;prj=common.datatestingvalidation.maps.yandex.net;signal=core-driving-router-over-osm_common_datatestingvalidation_maps_yandex_net;) | [rtc_balancer_common_datatestingvalidation_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_sas) <br>[rtc_balancer_common_datatestingvalidation_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_man) <br>[rtc_balancer_common_datatestingvalidation_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_vla) |
| Datavalidation | common_default | [core-driving-router-over-osm.common.datavalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datavalidation.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-driving-router-over-osm.common.datavalidation.maps.yandex.net"}) | [core-driving-router-over-osm.common.datavalidation.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datavalidation.maps.yandex.net;prj=common.datavalidation.maps.yandex.net;signal=core-driving-router-over-osm_common_datavalidation_maps_yandex_net;) | [rtc_balancer_common_datavalidation_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_sas) <br>[rtc_balancer_common_datavalidation_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_man) <br>[rtc_balancer_common_datavalidation_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_vla) |
| Stable | default | [core-driving-router-over-osm.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router-over-osm.maps.yandex.net/) | [core-driving-router-over-osm.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=core-driving-router-over-osm.maps.yandex.net;prj=core-driving-router-over-osm-maps;signal=service_total;) | [rtc_balancer_core-driving-router-over-osm_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router-over-osm_maps_yandex_net_sas) <br>[rtc_balancer_core-driving-router-over-osm_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router-over-osm_maps_yandex_net_vla) |
| Testing | common_default | [core-driving-router-over-osm.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-driving-router-over-osm.common.testing.maps.yandex.net"}) | [core-driving-router-over-osm.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-driving-router-over-osm_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |

### Firewall macroses

| staging | URL |
|---|---|
| Datatesting | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATATESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATATESTING_RTC_NETS_ ) |
| Datatestingvalidation | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATATESTINGVALIDATION_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATATESTINGVALIDATION_RTC_NETS_ ) |
| Datavalidation | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATAVALIDATION_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_DATAVALIDATION_RTC_NETS_ ) |
| Load | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_LOAD_RTC_NETS_ ) |
| Stable | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_OVER_OSM_TESTING_RTC_NETS_ ) |

## What happens when service is down

Users can't find shortest paths using desktop or mobile Yandex Maps. All navigations services built with MapKit are broken (Navigator, Taximeter, Yandex Maps and so on).

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/router/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2022-06-20` WHERE vhost LIKE 'core-driving-router-over-osm.maps.yandex.net' limit 1; |

| Log file | Logbroker topic |
|---|---|
| /var/log/nginx/access-tskv.log| [maps -> maps-log](https://logbroker.yandex-team.ru/logbroker/accounts/maps/maps-log) |
| /var/log/yandex/maps/router/router.log | [maps_router_over_osm -> prod -> router-log](https://logbroker.yandex-team.ru/logbroker/accounts/maps_router_over_osm/prod/router-log) |
| /var/log/yandex/maps/router/routes/tskv.log | [maps_router_over_osm -> prod -> route-geometry-log](https://logbroker.yandex-team.ru/logbroker/accounts/maps_router_over_osm/prod/route-geometry-log) |


## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[See troubleshooting.md for YMapsDF router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/troubleshooting.md)

## Documentation

[API](https://wiki.yandex-team.ru/maps/dev/core/routing/software/router/newrouterapi/)
[old description](https://wiki.yandex-team.ru/maps/dev/core/routing/software/router)

## Known clients

| Client | Firewall macros |
| ---- | --- |
| [Mobile proxy](https://abc.yandex-team.ru/services/maps-core-mobile/) | _MAPS_CORE_MOBILE_HTTP2_STABLE_RTC_NETS_ |
| Taxi | _TAXITESTNETS_, _HWTAXINETS_ |
| [Web](https://abc.yandex-team.ru/services/maps-front-router-service/) | _MAPSPRODQNETS_ |
| [B2B GEO routing public api](https://abc.yandex-team.ru/services/maps-b2bgeo-routing-public-api) | _B2BGEO_ROUTING_PUBLIC_API_STABLE_NETS_ |

## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
| [yandex-maps-geobase-tzdata](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-graph-osm-activator](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-osm-activator/versions) | [yandex-maps-graph-osm-activator](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-osm-activator/versions) |

## Persistent Volumes

* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_driving_router_over_osm.py)

## Regression tests

* Регрессионные стрельбы - OSM routing
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-driving-router-over-osm
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/712172
    * Тикет: https://st.yandex-team.ru/MAPSCORE-4985
Команда для сохранения патронов в Sandbox:
```ya upload --ttl=inf --type=AMMO_FILE --owner=MAPS --sandbox --description=<DESC> FILE_NAME```


Нагрузочные тесты через sedem не сконфигурированы. [Создать нагрузочные тесты](https://docs.yandex-team.ru/sedem/services/nanny#load-testing).

Sandbox-шедулер: [Общий шедулер регрессионных нагрузочных тестов](https://sandbox.yandex-team.ru/scheduler/702021)

Провести нагрузочный тест вручную:

+ воспользуйтесь кнопкой `Запустить` на [странице сервиса в SEDEM_SERVICE_PAGE в Sandbox](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-driving-router-over-osm%22%7D).
+ или возьмите [шаблон](https://sandbox.yandex-team.ru/template/MAPS_CORE_COMMON_LOAD_TESTING_TEMPLATE/view) —> нажмите `Create new task` —> наберите имя sedem-сервиса, уберите галочку «Run for all tests in service», наберите имя теста.

## Sandbox resources

https://sandbox.yandex-team.ru/resource/2918404323 - dummy-edge-speeds.pb compressed to resource.tar.gz

