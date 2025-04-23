# maps-core-stv-renderer

    Отдает тайлы слоя панорам в векторном и растровом формате

## General information

| Key | Value |
|---|---|
| Maintainers | https://staff.yandex-team.ru/idg <br/> https://staff.yandex-team.ru/orphean |
| SRE |  |
| Tracker Queue | MAPSPANO |
| Repository | https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/renderer |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_STV_RENDERER |
| RTC | maps-core-stv-renderer |
| ABC | https://abc.yandex-team.ru/services/maps-core-stv-renderer/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_renderer_testing/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_renderer_prestable/ |
| Production | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_renderer_stable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_renderer_load/ |

## Documentation

https://wiki.yandex-team.ru/maps/dev/core/streetview/

## Known clients

MAPS API https://wiki.yandex-team.ru/maps/api/
MAPKIT https://wiki.yandex-team.ru/maps/dev/core/mobile/mapkit2/


## Ecstatic datasets

http://ecstatic.maps.yandex.net/pkg/yandex-maps-streetview-bluelines/versions
http://ecstatic.maps.yandex.net/pkg/yandex-maps-streetview-design/versions


## What happens when service is down

Перестанут отображаться тайлы синих линий панорам на карте и в мапките.
Перестанут отображаться воздушные шарики панорам на карте и в мапките.
Перестанут показываться иконки возказов/аэропортов/метро в плеере панорам в мапките.

## How to fix common problems

Откатить датасет.

Рестартовать сервис: sudo yacare restart stv-renderer

## Балансеры
Production:
- Панели графиков с l7-балансеров: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-stv-renderer.maps.yandex.net;prj=core-stv-renderer-maps;ctype=prod;timelines=0.03,0.05,0.07,0.1,0.3,1;locations=sas,man,vla/
  - Метрики Порто контейнера балансера: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-stv-renderer.maps.yandex.net;prj=core-stv-renderer-maps;ctype=prod;locations=sas,man,vla/
- Собраны nanny-сервисы l7-балансеров:
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-renderer_maps_yandex_net_sas
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-renderer_maps_yandex_net_man
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-renderer_maps_yandex_net_vla
- Собраны AWACS-балансеры (описание и генератор конфигов l7-балансеров):
  - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-stv-renderer.maps.yandex.net
- Ссылка на ферму в l3manager: https://l3.tt.yandex-team.ru/service/6348
- Racktables: https://racktables.yandex-team.ru/?page=search&q=core-stv-renderer.maps.yandex.net
- Настройки файрвола: https://puncher.yandex-team.ru/?destination=core-stv-renderer.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Мониторинг балансеров: https://juggler.yandex-team.ru/?query=host%3Dsas.core-stv-renderer.maps.yandex.net%7Chost%3Dman.core-stv-renderer.maps.yandex.net%7Chost%3Dvla.core-stv-renderer.maps.yandex.net&statuses=WARN%2CCRIT%2COK

- Testing: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-stv-renderer-testing-slb


Balancers URL:
- Production: http://core-stv-renderer.maps.yandex.net
- Testing: http://core-stv-renderer.testing.maps.n.yandex.ru

## Мониторинги
| Type | URL |
|---|---|
| Juggler (all) | https://juggler.yandex-team.ru/?query=host%3Dsedem.maps.core-stv-renderer.stable%7Chost%3Dsedem.maps.core-stv-renderer.prestable%7Chost%3Dmaps_core_stv_renderer_testing |
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stv_renderer_stable |
| Juggler (Prestable) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stv_renderer_prestable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stv_renderer_testing |


## SLA
https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_stv_renderer
https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/#drugiegeoservisy


## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable+Prestable | [maps-core-stv-renderer-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stv-renderer-stable-panel-main) |
| Prestable | [maps-core-stv-renderer-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stv-renderer-prestable-panel-main) |
| Load | [maps-core-stv-renderer-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stv-renderer-load-panel-main) |
| Testing | [maps-core-stv-renderer-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stv-renderer-testing-panel-main) |

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| stv_renderer (сам сервис) | /var/log/yandex/maps/stv_renderer/* |
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-stv-renderer.maps.yandex.net' limit 1; |

## Firewall macroses
| staging | URL |
|---|---|
| stable | [_MAPS_CORE_STV_STABLE_RTC_NETS_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_STABLE_RTC_NETS_ ) |
| testing | [_MAPS_CORE_STV_TESTING_RTC_NETS_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSRENDER?service=stv_renderer
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/15629, https://sandbox.yandex-team.ru/scheduler/15639, https://sandbox.yandex-team.ru/scheduler/15641, https://sandbox.yandex-team.ru/scheduler/15643

