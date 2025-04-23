# <font color='red'>**ВНИМАНИЕ!!!** </font>

<font color='red'> **ПЕРЕД ИСПОЛЬЗОВАНИЕМ СЕРВИСА ОБЯЗАТЕЛЬНО СВЯЖИТЕСЬ С НАМИ.**

**ДЛЯ ИСПОЛЬЗОВАНИЯ СЕРВИСА НЕОБХОДИМО ДОГОВОРИТЬСЯ О КВОТЕ НА ЗАПРОСЫ,**
**ИНАЧЕ СЕРВИС МОЖЕТ НАЧАТЬ ОТВЕЧАТЬ 429 В САМЫЙ НЕОЖИДАННЫЙ МОМЕНТ.**
</font>
## Документация по новому API
https://wiki.yandex-team.ru/maps/dev/core/routing/software/router/newrouterapi/

## Старая документация
https://wiki.yandex-team.ru/maps/dev/core/routing/software/router

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Александр Агафонов [(@lokken)](https://staff.yandex-team.ru/lokken) <br/> Алексей Потапов [@avpotapov](https://staff.yandex-team.ru/@avpotapov) |
| Ответственные SRE | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Александр Агафонов [(@lokken)](https://staff.yandex-team.ru/lokken) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-driving-router/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_DRIVING_ROUTER |
| Исходники стрельб | https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsDrivingRouterShooting/ <br/> https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsNavistopwatchShooting/
| SEDEM panel | [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-driving-router%22%7D) |

## Instances
| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_stable |
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_prestable |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_datatesting |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_testing |
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_load |

| Dashboard |
|---|
| https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_driving_router |


## Known clients

- Mobile proxy (_C_MAPS_MOBILE_)
- Taxi (_TAXITESTNETS_)
- Media (_YNDXFORMEDIANETS_)
- Web (_C_MAPS_INT_)

## Graphics
| Type |
|---|
| [stable+prestable](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-stable-panel-main/) |
| [prestable](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-prestable-panel-main/) |
| [datavalidation](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-datavalidation-panel-main/) |
| [datatesting](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-datatesting-panel-main/) |
| [testing](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-testing-panel-main/) |
| [load](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-load-panel-main/) |

Для детальной диагностики так же можно посмотреть графики, предоставляемые Няней для каждого инстанса и детальные графики балансеров.

## Quotateka

* [Dashboard (stable)](https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_provider_dashboard/abc=maps-core-driving-router)
* [Dashboard (testing)](https://yasm.yandex-team.ru/template/panel/maps_core_quotateka_testing_provider_dashboard/abc=maps-core-driving-router)
* [Configuration in Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/quotateka/core-driving-router/)

## Monitorings
| Type | URL |
|---|---|
| stable (with prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_stable |
| prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_prestable |
| datavalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_datavalidation |
| datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_datatesting |
| testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_testing |
| load | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_router_load |

## Ecstatic datasets
* Граф
    * yandex-maps-graph-activator
    * yandex-maps-graph-compact
    * yandex-maps-graph-compact-edges-persistent-index
    * yandex-maps-graph-compact-rtree
    * yandex-maps-graph-router-data
    * yandex-maps-graph-router-topology
    * yandex-maps-graph-router-carparks
    * yandex-maps-graph-routing-barriers-rtree
* Пробки: 
  * yandex-maps-jams-speeds OR yandex-maps-jams-speeds-datatesting
  * yandex-maps-jams-closures OR yandex-maps-jams-closures-datatesting
  * yandex-maps-jams-speeds-forecast OR yandex-maps-jams-speeds-forecast-datatesting
* yandex-maps-geodata6
* yandex-maps-l6a-jams-diff
* yandex-maps-jams-edge-sequences-statistics
* yandex-maps-whole-track-models


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/spool/yandex/maps/graph - хардлинки на графы из экстатика
  * /var/spool/yandex/maps/closures/latest - симлинка на последнюю версию closures
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_DRIVING_ROUTER_STABLE_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_DRIVING_ROUTER_TESTING_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_ROUTER_TESTING_RTC_NETS_ ) |


## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Nginx | /var/log/nginx/* |
| Router | /var/log/yandex/maps/router/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/roquefort/* |
| YT  | https://yql.yandex-team.ru : select * from hahn.[//statbox/maps-router-log/2019-02-11] limit 5; (сюда упадут ВСЕ stable и prestable роутера в rtc - фильтруйте по полю source_uri)|

## Balancers
#### Production - core-driving-router.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/4255
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=5811
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/iXZWjYbmk/l3-vs-core-driving-router-maps-yandex-net
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_maps_yandex_net_man/ 
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_maps_yandex_net_vla/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-driving-router.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


#### Testing - core-driving-router.testing.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/4353
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=5896
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.testing.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/NcFck6-mk/l3-vs-core-driving-router-testing-maps-yandex-net
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.testing.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_testing_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_testing_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_testing_maps_yandex_net_vla/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-driving-router.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


#### Datavalidation - core-driving-router.datavalidation.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/10738
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=12063
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.datavalidation.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/O2OuyhvGz/l3-vs-core-driving-router-datavalidation-maps-yandex-net?orgId=1
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.datavalidation.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_datavalidation_maps_yandex_net_sas/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-driving-router.datavalidation.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


#### Datatesting - core-driving-router.datatesting.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/9920
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=11334
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.datatesting.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/9_khlkmMz/l3-vs-core-driving-router-datatesting-maps-yandex-net?orgId=1
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-driving-router.datatesting.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-driving-router_datatesting_maps_yandex_net_sas/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-driving-router.datatesting.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


## SLA
  * Criteries: https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_router.py
  * Statbox (new): https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_driving_router

## Regression Stress Testing Configurations
* Регрессионные стрельбы - routing
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=Router
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/447476
    * Тикет: https://st.yandex-team.ru/MAPSCORE-4647
* Регрессионные стрельбы - stopwatch
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-navistopwatch
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/10285/view
Команда для сохранения патронов в Sandbox:
```ya upload --ttl=inf --type=AMMO_FILE --owner=MAPS --sandbox --description=<DESC> FILE_NAME```

