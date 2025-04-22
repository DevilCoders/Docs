## Старая документация
https://wiki.yandex-team.ru/maps/dev/core/routing/graph-tile-builder

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Колганов Константин [(@kmkolganov)](https://staff.yandex-team.ru/kmkolganov) <br/> Александр Агафонов [(@lokken)](https://staff.yandex-team.ru/lokken)|
| Ответственные SRE | Константин Колганов [(@kmkolganov)](https://staff.yandex-team.ru/kmkolganov) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev)|
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-graph-tile-builder/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_GRAPH_TILE_BUILDER |
| Исходники стрельб | https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsGraphTileBuilderShooting <br/> https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsGraphTileBuilderAmmoGen/ |
|SEDEM SERVICE PAGE | https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-graph-tile-builder%22%7D |
|SEDEM RM auto-generated config| https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/release_machine/components/configs/sedem/maps_core_graph_tile_builder.py |

## Instances
| Dashboard |
|---|
| https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_graph_tile_builder/ |

| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_stable |
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_prestable |
| dataprestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_dataprestable |
| datavalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_datavalidation |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_testing |
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_load |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_graph_tile_builder_datatesting |

## Documentation
https://wiki.yandex-team.ru/maps/dev/core/routing/graph-tile-builder

## Known clients

- Mobile proxy

## Graphics
| Environment | URL |
|---|---|
| stable+prestable+dataprestable | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-stable-panel-main/ |
| prestable | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-prestable-panel-main/ |
| dataprestable | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-dataprestable-panel-main/ |
| datavalidation | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-datavalidation-panel-main/ |
| testing | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-testing-panel-main/ |
| load | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-load-panel-main/ |
| datatesting | https://yasm.yandex-team.ru/template/panel/maps-core-graph-tile-builder-datatesting-panel-main/ |

Для детальной диагностики так же можно посмотреть графики, предоставляемые Няней для каждого инстанса и детальные графики балансеров.

## Monitorings
| Environment | URL |
|---|---|
| stable (with prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host=maps_core_graph_tile_builder_stable |
| prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host=maps_core_graph_tile_builder_prestable |
| dataprestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_graph_tile_builder_dataprestable |
| datavalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_graph_tile_builder_datavalidation |
| testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host=maps_core_graph_tile_builder_testing |
| load | https://juggler.yandex-team.ru/aggregate_checks/?query=host=maps_core_graph_tile_builder_load |
| datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_graph_tile_builder_datatesting |

## Ecstatic datasets
* Граф
    * yandex-maps-graph-activator
    * yandex-maps-graph-compact
    * yandex-maps-graph-compact-rtree
* yandex-maps-mobile-driving-config-data

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся символические ссылки из:
    * /var/lib/yandex/maps/ecstatic - все данные экстатика
    * /var/spool/yandex/maps/graph - хардлинки на графы из экстатика
    * /var/cache/yandex/maps/graph-tile-builder - для хранения вспомогательного файла с поддерживаемыми версиями графа
    * /usr/share/yandex/maps/mapkit/driving/2.x - для хранения файла с версией графа мобильного конфига
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_GRAPH_TILE_BUILDER_STABLE_RTC_NETS_\_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GRAPH_TILE_BUILDER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_GRAPH_TILE_BUILDER_TESTING_RTC_NETS_\_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GRAPH_TILE_BUILDER_TESTING_RTC_NETS_ ) |
| datavalidation | [_\_MAPS_CORE_GRAPH_TILE_BUILDER_DATAVALIDATION_RTC_NETS_\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GRAPH_TILE_BUILDER_DATAVALIDATION_RTC_NETS_) |
| datatesting | [_\_MAPS_CORE_GRAPH_TILE_BUILDER_DATATESTING_RTC_NETS_\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GRAPH_TILE_BUILDER_DATATESTING_RTC_NETS_) |

## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Nginx | /var/log/nginx/* |
| graph-tile-builder | /var/log/yandex/maps/graph-tile-builder/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/maps/roquefort/* |
| YT | https://yql.yandex-team.ru : ``SELECT * FROM hahn.`logs/maps-log/1d/2019-04-02` WHERE (vhost = 'core-graph-tile-builder.maps.yandex.net' OR vhost = 'gt-builder.maps.yandex.net') AND request LIKE "/tile%" LIMIT 5;`` (сюда упадут ВСЕ stable, prestable и dataprestable gtb в rtc - фильтруйте по полю source_uri)|

## Balancers

#### Production - core-graph-tile-builder.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/5049
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=6380
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-graph-tile-builder.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/jzRFyflmk/l3-vs-core-graph-tile-builder-maps-yandex-net
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-graph-tile-builder.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_maps_yandex_net_vla/
  * Фаервол:
    * Доступы: https://puncher.yandex-team.ru/?destination=core-graph-tile-builder.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
    * Права: https://racktables.yandex-team.ru/index.php?page=services&tab=vperms#vs-6380

#### Testing - core-graph-tile-builder.testing.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/11047
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=12338
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-graph-tile-builder.testing.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/dashboard/db/l3-vs-core-graph-tile-builder-testing-maps-yandex-net
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-graph-tile-builder.testing.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_testing_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_testing_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-graph-tile-builder_testing_maps_yandex_net_vla/
  * Фаервол:
    * Доступы: https://puncher.yandex-team.ru/?destination=core-graph-tile-builder.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
    * Права: https://racktables.yandex-team.ru/index.php?page=services&tab=vperms#vs-12338

## SLA
  * Criteries: https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_graph_tile_builder.py
  * Statbox: https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_graph_tile_builder
  * Chart: https://charts.yandex-team.ru/preview/wizard/maps_SLA/maps_core_graph_tile_builder
  * Sandbox sheduler (see latest ran task): https://sandbox.yandex-team.ru/scheduler/11132/tasks

## Regression Stress Testing Configurations
* Регрессионные стрельбы
  * Lunapark: http://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-graph-tile-builder
  * Sandbox: https://sandbox.yandex-team.ru/scheduler/410799
  * Тикет: https://st.yandex-team.ru/MAPSCORE-4681

