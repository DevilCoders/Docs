# maps-jams-rdr
Отдает информацию о пробках и дорожных событиях.

**Table of Contents**
[TOC]

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Александр Любицкий (innocent@yandex-team.ru) Евгения Мордашова (morevi@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/renderer2/realtime |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-rdr |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_RDR |

## Instances, graphics, monitorings

| Staging       | Nanny service | Graphics panel | Monitoring checks |
| ------------- | ------------- | -------------- | ----------------- |
| Stable        | [maps_core_jams_rdr_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_stable) | [core-jams-rdr.stable](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-stable-panel-main/) | [maps_core_jams_rdr_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_stable&view=tiles&limit=200) |
| Prestable     | [maps_core_jams_rdr_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_prestable) | [core-jams-rdr.prestable](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-prestable-panel-main/) | [maps_core_jams_rdr_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_prestable&view=tiles&limit=200) |
| Testing       | [maps_core_jams_rdr_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_testing) | [core-jams-rdr.testing](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-testing-panel-main/) | [maps_core_jams_rdr_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_testing&view=tiles&limit=200) |
| Load          | [maps_core_jams_rdr_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_load) | [core-jams-rdr.load](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-load-panel-main/) | [maps_core_jams_rdr_load](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_load&view=tiles&limit=200) |
| Datatesting   | [maps_core_jams_rdr_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_datatesting) | [core-jams-rdr.datatesting](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-datatesting-panel-main/) | [maps_core_jams_rdr_datatesting](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_datatesting&view=tiles&limit=200) |

## Balancers

| Environment   | AWACS Balancer |
|---------------|----------------|
| Stable        | [core-jams-rdr.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr.maps.yandex.net) |
| Testing       | [core-jams-rdr.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-jams-rdr.common.testing.maps.yandex.net_default/show/) |

## Logs

| What | Where             |
|----------------|---------|
| Логи сервиса   | /var/log/yandex/maps/jams_renderer/jams_renderer.log |
| Создание карты | /var/log/yandex/maps/jams_renderer/jams_update.log |
| nginx          | /var/log/nginx/access-tskv.log |
| ecstatic       | /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log |
| YT             | `select * from hahn.[logs/maps-log/1d/{date}] where vhost = 'core-jams-rdr.maps.yandex.net'` |

## Increase cluster power by jams age degradation
Если на кластер приземляется слишком большая нагрузка, есть опция увеличить его производительность
за счет увеличения возраста пробок. Для этого нужно через dashboard сервиса установить переменные окружения (First group by: containters -> Environment variables configuration):
  * MAP_CREATION_PERIOD - периодичность генерации карт (должна быть кратна 30 секундам)
  * опционально JOINER_PARALLELIZATION - управляет количеством потоков, создаваемых при генерации карты. По-умолчанию выводится из предыдущего значения.

## Documentation
Сервис отдает картинку пробок в векторном либо растровом формате в виде тайлов и информацию о дорожных событиях.

**API**
|            |                                             |                                                              |
| ---------- | ------------------------------------------- | ------------------------------------------------------------ |
| /hotspots  | Returns hotspot tile for web                |                                                              |
| Params     | v                                           | Version of tile                                              |
|            | x, y, z                                     | Tile coordinates                                             |
|            | l                                           | Comma-separated tile layers (e.g. trf,chat,accident)         |
|            | locale                                      | Tile locale                                                  |
|            | callback                                    | Js callback (default "")                                     |
|            | style                                       | Map design (web, mobile, navi)                               |
|            |                                             |                                                              |
| /icons     | Returns icon image                          |                                                              |
| Params     | scale                                       | Icon image scale factor                                      |
|            | id                                          | Icon id returned in tile                                     |
|            | c1, c2, c3                                  | Primary, secondary, tertiary colors to customize icon (optional) |
|            |                                             |                                                              |
| /glyphs    | Returns sdf glyphs in protobuf format       |                                                              |
| Params     | font_id                                     | Font id returned in tile                                     |
|            | range                                       | Two comma-separated numbers specify range of glyph ids       |
|            |                                             |                                                              |
| /render    | Returns jams tile in specified format       |                                                              |
| Params     | v                                           | Version of tile                                              |
|            | x, y, z                                     | Tile coordinates                                             |
|            | l                                           | Comma-separated tile layers (e.g. trf,chat,accident)         |
|            | vec_protocol                                | Protobuf tile format version (ignored for images, default 2) |
|            | zmin, zmax                                  | Zoom range for multizoom tiles (ignored for images, default z) |
|            | scale                                       | Tile image scale factor (ignored for protobuf)               |
|            | style                                       | Map design (web, mobile, navi)                               |
|            | theme                                       | Map theme. Values: dark, light (ignored for protobuf, default light) |
|            | experimental_trf_design                     | Map design from Cartograph experimental branch. Use special value 'testing' instead of exp id, to view design testing |
|            | format                                      | Tile format, has a higher priority than Accept. Values: protobuf, png, text |
| Headers    | Accept                                      | Specify tile format (application/x-protobuf, image/png, text/x-protobuf) |
|            |                                             |                                                              |
| /1.0/tiles | Converted to /render with png format        | See /render?format=png                                       |
| Params     | tm                                          | See 'v' param in /render                                     |
|            |                                             |                                                              |
| /1.1/tiles | Converted to /render with png format        | See /render?format=png                                       |
| Params     | tm                                          | See 'v' param in /render                                     |
|            |                                             |                                                              |
| /2.x/tiles | Converted to /render with protobuf format   | See /render?format=protobuf                                  |
| Params     | tm                                          | See 'v' param in /render                                     |
|            |                                             |                                                              |
| /version   | Returns current map version                 |                                                              |
| Params     | format                                      | Content type, has a higher priority than Accept. Values: protobuf, text, xml |
| Headers    | Accept                                      | Specify format (application/x-protobuf, text/x-protobuf, image/png) |
|            |                                             |                                                              |
| /info      | Returns information about traffic situation |                                                              |
| Params     | format                                      | Info format, has a higher priority than Accept. Values: protobuf, xml, js |
| Headers    | Accept                                      | Specify format (application/x-protobuf, application/xml, application/javascript) |

## Known client
[Maps-mobile](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/) <br>
[Maps.API](https://tech.yandex.com/maps/) <br>
[Yandex Maps](http://maps.yandex.ru)

## Ecstatic datasets
* Граф
  * yandex-maps-graph-activator
  * yandex-maps-graph-compact
  * yandex-maps-graph-compact-rtree
  * yandex-maps-graph-edges-persistent-index

* Пробки
  * yandex-maps-jams-speeds
  * yandex-maps-jams-speeds-external
  * yandex-maps-jams-closures
  * yandex-maps-jams-events

* yandex-maps-jams-design
* yandex-maps-geodata6
* yandex-maps-geobase-tzdata
* yandex-maps-coverage5-geoid
* yandex-maps-coverage5-trf

## Firewall macroses
| Staging | URL            |
|---------------|----------|
| Stable  | [\_MAPS_CORE_JAMS_RDR_STABLE_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_STABLE_RTC_NETS_) |
| Testing | [\_MAPS_CORE_JAMS_RDR_TESTING_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_TESTING_RTC_NETS_) |

## What happens when service is down
Пробки на мобильных и на вебе не отображаются или отображаются некорректно.

## How to fix common problems
Посмотреть все ли ок с генерацией карты: `tail -f /var/log/yandex/maps/jams_renderer/jams_update.log`
Если что-то падает скорее всего или не хватает данных, или какие-то данным сломаны, смотреть ecstatic.
Посмотреть, не залипли ли датасеты с пробками: http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-jams-speeds/versions
Если хотя бы один шард не раскладывается, карты перестанут создаваться.

Посмотреть логи сервиса: `tail -f /var/log/yandex/maps/jams_renderer/jams_renderer.log`
Если сервис не может подняться, может быть испорчена какая-то карта, нужно их поудалять: `rm -r /var/lib/yandex/maps/jams/renderer2/maps/201*`

## Secrets

https://nanny.yandex-team.ru/ui/#/keychains/core-jams-rdr.maps.yandex.net/secrets

## Design

Дизайны публикуются из Картографа https://cartograph.maps.yandex-team.ru (доступен для [abc:cartographusers](https://abc.yandex-team.ru/services/cartographusers)). Датасет с дизайном [yandex-maps-jams-design](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-jams-design/versions) создает модуль Огорода [design_bundles](https://garden.maps.yandex-team.ru/stable/design_bundles) и активирует модуль [jams_design_deployment](https://garden.maps.yandex-team.ru/stable/jams_design_deployment).

Тестинг дизайна (это не тестинг софта, а релиз-кандидат дизайна) доступен под экспериментом в БЯК и inhouse-сборках приложений:
- БЯК: https://yandex.ru/maps?l=trf,trfe&renderer_experimental_trf_design=testing
- [МЯК](https://beta.m.soft.yandex.ru/maps/master): `yandexmaps://add_exp/MAPS_RENDERER?experimental_trf_design=testing`
- [Навигатор](https://beta.m.soft.yandex.ru/ynavi/release): `yandexnavi://add_exp/MAPS_RENDERER?experimental_trf_design=testing`

Чтобы протестировать доработки в модулях Огорода, нужно:
- выкатить модули огорода в [дататестинг](https://garden.maps.yandex-team.ru/datatesting/design_bundles)
- опубликовать какой-нибудь дизайн в [тестинге Картографа](https://cartograph.tst.c.maps.yandex-team.ru)
- протестировать пробки в дататестинге в БЯК: https://l7test.yandex.ru/maps?l=trf,trfe&renderer_experimental_datatesting=1
- протестировать пробки в дататестинге в сборке [release_stesting Навигатора](https://beta.m.soft.yandex.ru/ynavi/release_stesting): `yandexnavi://add_exp/MAPS_RENDERER?experimental_datatesting=1`

## SLA
Правильно обслуживаются 99.9% запросов в месяц. <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_rdr.py) <br>
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_jams_rdr)

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=jams_renderer |
| CI |                                                     |
| Тайминги | https://sandbox.yandex-team.ru/scheduler/19092/view |
| Разладка | https://sandbox.yandex-team.ru/scheduler/19093/view |
