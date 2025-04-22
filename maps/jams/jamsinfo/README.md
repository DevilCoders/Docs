# maps-jams-info
Информация о пробках и экспорт

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Дмитрий Раздобарин (topq@yandex-team.ru)  Александр Любицкий (innocent@yandex-team.ru) Евгения Мордашова (morevi@yandex-team.ru) |
| SRE | Дмитрий Раздобарин (topq@yandex-team.ru)  |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/jamsinfo |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-info |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_INFO |

## Instances

| Environment   | URL                                                          |
| ------------- | ------------------------------------------------------------ |
| **Dashboard** | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps-jams-info |
| Testing       | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_info_testing |
| Load          | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_info_load |
| Prestable     | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_info_prestable |
| Stable        | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_info_stable |

## Balancers

| Environment   | URL      |
|---------------|----------|
| Stable        | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-info.maps.yandex.net |
| Testing       | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-info.testing.maps.yandex.net |

Некоторую часть запросов балансер отправляет в сервис mediascreens, см. соответсвующий upstream:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-info.maps.yandex.net/upstreams/list/mediascreens/show

Так же, для поддержки старого API, в балансере настроены rewrite'ы, см. upstream:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-info.maps.yandex.net/upstreams/list/default/show

## Graphics

| Staging | URL            |
|---------------|----------|
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-jams-info-stable-panel-main |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-jams-info-testing-panel-main |

## Logs

| What | Where             |
|----------------|---------|
| Логи сервиса   | /var/log/yandex/maps/jams_renderer/jamsinfo.log |
| Создание карты | /var/log/yandex/maps/jams_renderer/jams_update.log |
| nginx          | /var/log/nginx/access-tskv.log |
| ecstatic       | /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log |
| YT             | `select * from hahn.[logs/maps-log/1d/{date}] where vhost = 'core-jams-info.maps.yandex.net'` |

**API**
|           |                                             |                                                              |
| --------- | ------------------------------------------- | ------------------------------------------------------------ |
| /info     | Returns jams info for all available regions |                                                              |
| Params    | format                                      | Response format (xml, js, json, proto, legacy_navi)          |
|           | callback                                    | jsonp callback from json request (available for json format) |
|           | ids                                         | coma separated list of region ids                            |
| Headers   | Accept                                      | Specify tile format (application/x-protobuf, image/png, text/x-protobuf) |
|           |                                             |                                                              |
| /export   | Returns wide jams info for region           |                                                              |
| Params    | region_id                                   | Requested region                                             |
|           | id                                          | Icon id returned in tile                                     |
|           |                                             |                                                              |
| /coverage | Returns traffic coverage info               |                                                              |
| Params    | version                                     | Version of tile                                              |

## Known client
[Maps-mobile](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/) <br>
[Maps.API](https://tech.yandex.com/maps/) <br>
[Yandex Maps](http://maps.yandex.ru)
Морда яндекса
Внешние пользователи данных (?? кто)

## ecstatic Datasets
* Граф
  * yandex-maps-graph-activator
  * yandex-maps-graph-compact
  * yandex-maps-graph-compact-rtree
  * yandex-maps-graph-edges-persistent-index

* Пробки
  * yandex-maps-jams-speeds
  * yandex-maps-jams-closures
  * yandex-maps-jams-historic-levels

* Прогноз баллов
  * yandex-maps-calendar
  * yandex-maps-jams-level-history
  * yandex-maps-jams-level-prediction-model
  * yandex-maps-geobase-tzdata

* yandex-maps-coverage5-geoid
* yandex-maps-coverage5-trf
* yandex-maps-geodata6

## Firewall macroses
| Staging | URL            |
|---------------|----------|
| Stable  | [\_MAPS_CORE_JAMS_INFO_STABLE_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFO_STABLE_RTC_NETS_) |
| Testing | [\_MAPS_CORE_JAMS_INFO_TESTING_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFO_TESTING_RTC_NETS_) |

## What happens when service is down
Приходят с морды и жалуются, что пробки не обновляются
Возможно, придет кто-то еще

## How to fix common problems
Посмотреть все ли ок с генерацией карты: `tail -f /var/log/yandex/maps/jams_renderer/jams_update.log`
Если что-то падает скорее всего или не хватает данных, или какие-то данным сломаны, смотреть ecstatic.
Посмотреть, не залипли ли датасеты с пробками: http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-jams-speeds/versions
Если хотя бы один шард не раскладывается, карты перестанут создаваться.

Посмотреть логи сервиса: `tail -f /var/log/yandex/maps/jams_renderer/jamsinfo.log`
Для старта сервиса необходим датасет с геодатой. Запускается сервис в соответствующем хуке, при проблемах с ecstatic'ом ничего работать не будет.
В таком случае можно руками положить данные куда надо (см. хуки геодаты) и запустить сервис.

## Secrets

ssl: https://nanny.yandex-team.ru/ui/#/keychains/core-jams-info.maps.yandex.net/secrets
tvm secret: https://yav.yandex-team.ru/secret/sec-01dh8tknd5g9jj74zrpcqbq0pr

## Monitorings

| Staging | URL            |
|---------------|----------|
| Stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_info_stable |
| Testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_info_testing |

## Archived jams info
**Logbroker**
| Staging | URL            |
|---------------|----------|
| Stable | https://lb.yandex-team.ru/main/topic/maps-core-jams-info%2Fproduction%2Flevels |
| Testing | https://lb.yandex-team.ru/main/topic/maps-core-jams-info%2Ftesting%2Flevels |

**YT**
| Staging | URL            |
|---------------|----------|
| Stable | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-info-production-levels/1d |
| Testing | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-info-testing-levels/1d |


## SLA
Правильно обслуживаются 99.9% запросов в месяц. <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_info.py) <br>
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_jams_info)

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSJAMS?service=jamsinfo |
| CI |                                                     |
| Разладка | https://sandbox.yandex-team.ru/scheduler/17710 |


