# maps-core-stvdescr

    Выдает описания панорам для отображения плеером.
    Ищет ближайшие панорамы.

## General information

| Key | Value |
|---|---|
| Maintainers | https://staff.yandex-team.ru/idg <br/> https://staff.yandex-team.ru/orphean |
| SRE |  https://staff.yandex-team.ru/idg <br/> https://staff.yandex-team.ru/orphean |
| Tracker Queue | MAPSPANO |
| Repository | https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/description |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_MAPS_CORE_STVDESCR_DOCKER |
| RTC | maps-core-stvdescr |
| ABC | https://abc.yandex-team.ru/services/maps-core-panoramas-proxy/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stvdescr_testing/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stvdescr_prestable/ |
| Production | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stvdescr_stable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stvdescr_load/ |

## Documentation

https://wiki.yandex-team.ru/maps/dev/core/streetview/

## Known clients

MAPS API https://wiki.yandex-team.ru/maps/api/
MAPKIT https://wiki.yandex-team.ru/maps/dev/core/mobile/mapkit2/


## Ecstatic datasets

http://ecstatic.maps.yandex.net/pkg/yandex-maps-streetview-description/versions
http://ecstatic.maps.yandex.net/pkg/yandex-maps-streetview-address/versions


## What happens when service is down

Перестанут искаться ближайшие панорамы в мапките.
Перестанут открываться панорамы в MAPS API и MAPKIT.

## How to fix common problems

Теоретически работу сервиса может поломать кривой датасет yandex-maps-streetview-description или yandex-maps-streetview-address.

В таком случае можно откатить датасет, поставив симлинку на прошлую версию.

Рестартовать сервис: sudo yacare restart streetview-description

## Балансеры
Production:
- Панели графиков с l7-балансеров: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-stvdescr.maps.yandex.net;prj=core-stvdescr-maps;ctype=prod;timelines=0.03,0.05,0.07,0.1,0.3,1/
  - Метрики Порто контейнера балансера: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-stvdescr.maps.yandex.net;prj=core-stvdescr-maps;ctype=prod/
- Собраны nanny-сервисы l7-балансеров:
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stvdescr_maps_yandex_net_man
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stvdescr_maps_yandex_net_sas
  - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stvdescr_maps_yandex_net_vla
- Собраны AWACS-балансеры (описание и генератор конфигов l7-балансеров):
  - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-stvdescr.maps.yandex.net
- Ссылка на ферму в l3manager: https://l3.tt.yandex-team.ru/service/3708
- Racktables: https://racktables.yandex-team.ru/?page=search&q=core-stvdescr.maps.yandex.net
- Настройки файрвола: https://puncher.yandex-team.ru/?destination=core-stvdescr.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Мониторинг балансеров: https://juggler.yandex-team.ru/?query=host%3Dsas.core-stvdescr.maps.yandex.net%7Chost%3Dman.core-stvdescr.maps.yandex.net%7Chost%3Dvla.core-stvdescr.maps.yandex.net&statuses=WARN%2CCRIT%2COK

- Testing: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-stvdescr-testing-slb


Balancers URL:
- Production: http://core-stvdescr.maps.yandex.net
- Testing: http://core-stvdescr.testing.maps.n.yandex.ru

## Мониторинги
| Type | URL |
|---|---|
| Juggler (all) | https://juggler.yandex-team.ru/?query=host%3Dsedem.maps.core-stvdescr.stable%7Chost%3Dsedem.maps.core-stvdescr.prestable%7Chost%3Dmaps_core_stvdescr_testing |
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stvdescr_stable |
| Juggler (Prestable) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stvdescr_prestable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_stvdescr_testing |


## SLA
https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_stvdescr
https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/#drugiegeoservisy


## Графики
| Staging | Golovan panel URL |
|---|---|
| Панель сервиса| https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-stable-panel-main/ |
| Tiles s3-mds | [Tiles s3-mds](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=pano;owner=1984?range=86400000) |
| Stable+Prestable | [maps-core-stvdescr-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-stable-panel-main) |
| Prestable | [maps-core-stvdescr-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-prestable-panel-main) |
| Load | [maps-core-stvdescr-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-load-panel-main) |
| Testing | [maps-core-stvdescr-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-testing-panel-main) |

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| streetview description (сам сервис) | /var/log/yandex/maps/streetview-description/* |
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : select * from hahn.[home/logfeller/logs/maps-log/1d/2018-02-28] where tskv_format='stvdescr' |


## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSPANO |

