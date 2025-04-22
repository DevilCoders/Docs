# Core Driving Matrix Router Over Osm

Матричный роутер поверх OSM - это сервис, который вычисляет матрицу расстояний и времен проезда на автомобиле или грузовике между множеством исходных и конечных точек. Расстояния и времена вычисляются на графе, построенном на основе OSM-данных.

## General information
| What | Who |
|---|---|
| Ответственные разработчики | Александр Игнатьев [(@asi81)](https://staff.yandex-team.ru/asi81) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Константин Колганов [(kmkolganov)](https://staff.yandex-team.ru/kmkolganov) <br/> Игорь Мартынов [(@immartynov)](https://staff.yandex-team.ru/immartynov) |
| Ответственные SRE | Игорь Мартынов [(@immartynov)](https://staff.yandex-team.ru/immartynov) <br/> Константин Колганов [(@kmkolganov)](https://staff.yandex-team.ru/kmkolganov) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) |
| Исходники | [maps/routing/matrix_router/osm](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/osm) |
| Сервис в ABC | [maps-core-driving-matrix-router-over-osm](https://abc.yandex-team.ru/services/maps-core-driving-matrix-router-over-osm/)|
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM |
| SEDEM panel | [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={"sedem_service":%20"core-driving-matrix-router-over-osm"}) |
| API | https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/README.md |

## End-points

| Staging | URL |
|---------|-----|
| Stable | http://core-driving-matrix-router-over-osm.maps.yandex.net/ |
| Testing | http://core-driving-matrix-router-over-osm.common.testing.maps.yandex.net/ |
| DataValidation | http://core-driving-matrix-router-over-osm.common.datavalidation.maps.yandex.net/ |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Datavalidation | [maps_core_driving_matrix_router_over_osm_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_datavalidation/) | [ core-driving-matrix-router-over-osm.datavalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-datavalidation-panel-main/) | [ maps_core_driving_matrix_router_over_osm_datavalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_datavalidation) |
| Load | [maps_core_driving_matrix_router_over_osm_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_load/) | [ core-driving-matrix-router-over-osm.load ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-load-panel-main/) | [ maps_core_driving_matrix_router_over_osm_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_load) |
| Prestable | [maps_core_driving_matrix_router_over_osm_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_prestable/) | [ core-driving-matrix-router-over-osm.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-prestable-panel-main/) | [ maps_core_driving_matrix_router_over_osm_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_prestable) |
| Stable | [maps_core_driving_matrix_router_over_osm_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_stable/) | [ core-driving-matrix-router-over-osm.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-stable-panel-main/) | [ maps_core_driving_matrix_router_over_osm_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_stable) |
| Testing | [maps_core_driving_matrix_router_over_osm_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_testing/) | [ core-driving-matrix-router-over-osm.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-testing-panel-main/) | [ maps_core_driving_matrix_router_over_osm_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_testing) |
| Unstable | [maps_core_driving_matrix_router_over_osm_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_over_osm_unstable/) | [ core-driving-matrix-router-over-osm.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-unstable-panel-main/) | [ maps_core_driving_matrix_router_over_osm_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_unstable) |

[Monitorings all (tag=a_prj_maps-core-driving-matrix-router-over-osm)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-driving-matrix-router-over-osm)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-driving-matrix-router-over-osm.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-matrix-router-over-osm.maps.yandex.net/) | [core-driving-matrix-router-over-osm.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-driving-matrix-router-over-osm.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=core-driving-matrix-router-over-osm-maps;signal=service_total) | [rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_man)<br>[rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_sas)<br>[rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-matrix-router-over-osm_maps_yandex_net_vla) |

## What happens when service is down

Если сервис не работает, то клиенты не смогут строить матрицы расстояний в зарубежных странах на основе OSM-данных. Тогда сервисы доставки не смогут построить план развоза товаров и решить задачу коммивояжёра.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| matrix-router | /var/log/yandex/maps/matrix_router/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Push-client | /var/log/statbox/* |
| Roquefort | /var/log/yandex/maps/roquefort/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-09-01` WHERE vhost = 'core-driving-matrix-router-over-osm.maps.yandex.net' LIMIT 1; |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-matrix-router-over-osm-log/1d/2021-09-02` WHERE url_path = '/v2/matrix' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc) <br/>
[troubleshooting.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/osm/troubleshooting.md)

## Documentation

[Построение статистических скоростей для матричного роутера (для справки)](https://wiki.yandex-team.ru/maps/dev/core/routing/postroenie-stat.-skorostejj-dlja-matrichnyx-zaprosov/?from=%2Fmaps%2Fdev%2Fcore%2Frouting%2Fdefaultspeeds%2Fpostroenie-stat.-skorostejj-dlja-matrichnyx-zaprosov%2F) <br/>
[Sharding](https://wiki.yandex-team.ru/maps/dev/core/routing/sharding)<br/>
[Примеры запросов](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/README.md#primery-zaprosov)

## Known clients
| Client | TVM id | Network macroses |
|---|---|---|
| B2B Geo| 2011656 | \_B2BGEO_ROUTING_PUBLIC_API_STABLE_NETS\_, \_B2BGEO_YA_COURIER_PROD_NETS\_ |

### Ratelimiter
* [Golovan Ratelimiter panel for stable](https://yasm.yandex-team.ru/template/panel/maps_core_driving_matrix_router_over_osm-ratelimiter2-panel/)
* [Ratelimiter configs in Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_driving_matrix_router_over_osm)

## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
| [yandex-maps-osm-graph-speed-profiles](http://ecstatic.maps.yandex.net/pkg/yandex-maps-osm-graph-speed-profiles/versions) | [yandex-maps-osm-graph-speed-profiles](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-osm-graph-speed-profiles/versions) |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-geobase-tzdata](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_driving_matrix_router_over_osm) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_driving_matrix_router_over_osm.py)

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_STABLE_RTC_NETS_ ) |
| datavalidation | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_DATAVALIDATION_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_DATAVALIDATION_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_TESTING_RTC_NETS_ ) |
| load | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_OVER_OSM_LOAD_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы по матричному роутеру поверх OSM
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-driving-matrix-router-over-osm
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/695987
    * [Datalens](https://datalens.yandex-team.ru/hckadjiuwrf8a-maps-sla-dashboard?state=1820384a166)
    * Тикет: https://st.yandex-team.ru/MAPSCORE-4912


## Внешние зависимости

### MDS
Результат обработки асинхронных запросов загружается в MDS, а клиент получает ссылку на скачивание из MDS

| Environment | bucket project id | Dashboard | Alert |
|---|---|---|---|
| production | matrix-router-osm-result | [MDS space usage](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=matrix-router-osm-result)<br> [MDS proxy statuses](https://yasm.yandex-team.ru/template/panel/mds_proxy/ns=matrix-router-osm-result) | [MDS quota usage](https://juggler.yandex-team.ru/check_details/?host=maps_core_driving_matrix_router_over_osm_stable&service=mds-disk-quota-perc-usage-matrix-router-osm-result&last=1DAY)<br> [MDS 4xx (prestable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-prestable)<br> [MDS 4xx (stable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-stable)<br> [MDS 5xx (prestable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-prestable)<br> [MDS 5xx (stable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-stable) |
| testing | matrix-router-result-testing | [MDS space usage](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=matrix-router-result-testing) | [MDS quota usage](https://juggler.yandex-team.ru/check_details/?host=maps_core_driving_matrix_router_testing&service=mds-disk-quota-perc-usage-matrix-router-result-testing&last=1DAY)<br> [MDS 4xx (testing)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-testing)<br> [MDS 5xx (testing)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-testing) |

### MDB

| Environment | Cluster id | Monitorings |
|---|---|---|
| stable | [mdbpr4uhr1vq2ir3tlhb](https://yc.yandex-team.ru/folders/akuoltivee0h99g1ne08/managed-mongodb/cluster/mdbpr4uhr1vq2ir3tlhb) | [mongo-mdb alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_stable%26service%3Dmongodb-mdb-*) |
| datavalidation | [mdb641hbatfm5bvlt66f](https://yc.yandex-team.ru/folders/akuoltivee0h99g1ne08/managed-mongodb/cluster/mdb641hbatfm5bvlt66f) | [mongo-mdb alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_datavalidation%26service%3Dmongodb-mdb-*) |
| testing | [mdbkqm0aqv20bqe4iq2p](https://yc.yandex-team.ru/folders/akuoltivee0h99g1ne08/managed-mongodb/cluster/mdbkqm0aqv20bqe4iq2p) | [mongo-mdb alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_testing%26service%3Dmongodb-mdb-*) |
| load | [mdbr0v8v0vajsgdtf15t](https://yc.yandex-team.ru/folders/akuoltivee0h99g1ne08/managed-mongodb/cluster/mdbr0v8v0vajsgdtf15t) | [mongo-mdb alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_over_osm_load%26service%3Dmongodb-mdb-*) |

### Logbroker

| Environment | Log | Account | Topic | Log on YT |
|---|---|---|---|---|
| stable| /var/log/yandex/maps/matrix_router/matrix_router.log | [maps_matrix_router_over_osm](https://lb.yandex-team.ru/logbroker/accounts/maps_matrix_router_over_osm) | [maps-matrix-router-log](https://lb.yandex-team.ru/logbroker/accounts/maps_matrix_router_over_osm/prod/maps-matrix-router-log) | [//logs/maps-matrix-router-over-osm-log/1d/](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-matrix-router-over-osm-log/1d) |

## MapsMatrixRouterShooting (shooter)

Таска тестирования матричного роутера:  
https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsMatrixRouterShootingTask

Планировщик таски тестирования матричного роутера:  
https://sandbox.yandex-team.ru/scheduler/699956/view

Агрегат в джаглере:  
https://juggler.yandex-team.ru/check_details/?host=sandbox.MapsMatrixRouterShootingTask.osm&service=shooting_failed&project=maps&last=1DAY  
`host=sandbox.MapsMatrixRouterShootingTask.osm & service=shooting_failed`
