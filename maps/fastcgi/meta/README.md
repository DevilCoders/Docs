# maps-core-meta

Выдаёт информацию о наличии слоёв и их метаинформацию в точке/области.

[TOC]

## General information

| Key | Value |
| --- | ----- |
| Кому звонить, если ничего не понятно | [Илья Власюк](https://staff.yandex-team.ru/tail), [Дмитрий Сухов](https://staff.yandex-team.ru/quoter), [Борис Чикунов](https://staff.yandex-team.ru/chikunov) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/fastcgi/meta |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-meta/ |
| Покоммитная сборка докер-образов | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_META |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Dataprestable | [maps_core_meta_dataprestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_dataprestable/) | [ core-meta.dataprestable ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-dataprestable-panel-main/) | [ maps_core_meta_dataprestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_dataprestable) |
| Datatesting | [maps_core_meta_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_datatesting/) | [ core-meta.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-datatesting-panel-main/) | [ maps_core_meta_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_datatesting) |
| Datatestingvalidation | [maps_core_meta_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_datatestingvalidation/) | [ core-meta.datatestingvalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-datatestingvalidation-panel-main/) | [ maps_core_meta_datatestingvalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_datatestingvalidation) |
| Datavalidation | [maps_core_meta_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_datavalidation/) | [ core-meta.datavalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-datavalidation-panel-main/) | [ maps_core_meta_datavalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_datavalidation) |
| Load | [maps_core_meta_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_load/) | [ core-meta.load ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-load-panel-main/) | [ maps_core_meta_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_load) |
| Prestable | [maps_core_meta_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_prestable/) | [ core-meta.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-prestable-panel-main/) | [ maps_core_meta_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_prestable) |
| Stable | [maps_core_meta_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_stable/) | [ core-meta.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-stable-panel-main/) | [ maps_core_meta_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_stable) |
| Testing | [maps_core_meta_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_meta_testing/) | [ core-meta.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-meta-testing-panel-main/) | [ maps_core_meta_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_meta_testing) |


[Monitorings all (tag=a_prj_maps-core-meta)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-meta)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Datatesting | Default | [core-meta.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-meta.datatesting.maps.yandex.net/) | [core-meta.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-meta.datatesting.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=core-meta-datatesting-maps;signal=service_total) | [rtc_balancer_core-meta_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datatesting_maps_yandex_net_man)<br>[rtc_balancer_core-meta_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datatesting_maps_yandex_net_sas)<br>[rtc_balancer_core-meta_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datatesting_maps_yandex_net_vla) |
| Datatestingvalidation | Default | [core-meta.common.datatestingvalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatestingvalidation.maps.yandex.net/show/) | | | 
| Datavalidation | Default | [core-meta.datavalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-meta.datavalidation.maps.yandex.net/) | [core-meta.datavalidation.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-meta.datavalidation.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=core-meta-datavalidation-maps;signal=service_total) | [rtc_balancer_core-meta_datavalidation_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datavalidation_maps_yandex_net_man)<br>[rtc_balancer_core-meta_datavalidation_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datavalidation_maps_yandex_net_sas)<br>[rtc_balancer_core-meta_datavalidation_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-meta_datavalidation_maps_yandex_net_vla) |
| Stable | Default | [core-meta.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-meta.maps.yandex.net/) | [core-meta.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-meta.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=core-meta-maps;signal=service_total) | [production_balancer_core_meta_maps_man](https://nanny.yandex-team.ru/ui/#/services/catalog/production_balancer_core_meta_maps_man)<br>[production_balancer_core_meta_maps_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_balancer_core_meta_maps_sas)<br>[production_balancer_core_meta_maps_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_balancer_core_meta_maps_vla) |
| Testing | Default | [core-meta.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-meta.common.testing.maps.yandex.net_default/show/) | [core-meta_common_testing_maps_yandex_net_default](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=common.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=common.testing.maps.yandex.net;signal=core-meta_common_testing_maps_yandex_net_default;) | |

## Known clients

* [meta-int](https://wiki.yandex-team.ru/maps/api/http/internal/meta)
* [coverage-api](https://github.yandex-team.ru/mapsapi/coverage-api)
* [Static Maps API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi)

## ecstatic datasets

* yandex-maps-data-vec
* yandex-maps-coverage5-geoid
* yandex-maps-coverage5-trf
* yandex-maps-coverage5-metro
* yandex-maps-coverage5-router
* yandex-maps-coverage5-spots
* yandex-maps-coverage5-streetview
* yandex-maps-coverage5-sat
* yandex-maps-renderer-blacklist-version

## What happens when service is down

На maps.yandex.ru исчезнет информация о доступности пробок, маршрутизации, парковок, зумах карты. Скорее всего верстка maps.yandex.ru полностью перестанет работать.
Деградации не предусмотрены.

## How to fix common problems

* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc).
* Смотри также пример [mobmaps-proxy-api](https://github.yandex-team.ru/mapsapi/mobmaps-proxy#how-to-fix-common-problems).


## SLA

[Отчёт в stat](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_meta)

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
| ---- | -------- |
| nginx | `/var/log/nginx` |
| dorblu agent | `/var/log/yandex/geo-dorblu-agent` |
| yacare| `/var/log/yandex/maps/yacare` |
| meta | `/var/log/yandex/maps/meta` |
| ecstatic | `/var/log/yandex/maps/ecstatic-agent` |
| supervisord | `/var/log/supervisor` |
| syslog (unfiltered) | `/var/log/syslog` |
| [YT](https://yql.yandex-team.ru) | ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/{date}` WHERE tskv_format = 'meta' ``` (сюда упадут ВСЕ меты - фильтруйте по полю `source_uri`) |

## Regression Stress Testing Configurations

| Type | URL |
| ---- | --- |
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-meta |
| Imbalance | https://sandbox.yandex-team.ru/scheduler/8831/view |
| Timings | https://sandbox.yandex-team.ru/scheduler/10233/view |

## API

API состоит из одной ручки: `GET /layers`.

### Параметры вызова

* `action`: действие, на данный момент поддерживается только `info` (обязательный параметр)
* `l`: слои: map/sat/skl/trf (string,[string]...)https://wiki.yandex-team.ru/maps/dev/core/servants/Mapmeta/
* `ll`: долгота, широта в градусах (float, float)
* `spn`:
* `bbox`:
* `z`: масштаб [0–23] (uint)

### GET /layers

Возвращаемый ответ варьируется в зависимости от переданных параметров:

* `action=info` + `l`: для каждого слоя из параметра `l` возвращает текущую версию и метаданные слоёв
* `action=info` + `l` + `ll`: для каждого слоя из параметра `l` возвращает `zmin`, `zmax`, список копирайтов в точке, а также метаданные самого слоя
* `action=info` + `l` + `ll` + `z`: для каждого слоя из параметра `l`, для которого `zmax` >= `z`, выдаёт список копирайтов в точке, а также метаданные самого слоя
* `action=info` + `l` + `ll` + `spn` + `z` (optional): фильтрует список слоёв по признаку присутствия данного слоя в указанном bbox. Параметр `z` является опциональным (для некоторых слоёв — обязательным, список определяется конфигом).
* `action=info` + `l` + `bbox` + `z` (optional): аналогично предыдущему вызову

Информация [о слоях вообще](https://wiki.yandex-team.ru/maps/dev/core/layers/description/), [о доступных](https://wiki.yandex-team.ru/maps/dev/core/layers/current.layers/) на данный момент слоях в частности.
