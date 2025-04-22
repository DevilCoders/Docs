# Road events renderer
[[toc]]

## About

Рендерер слоя дорожных событий.
"Старый слой" TrafficLayer (vmap2) обслуживает мобильных клиентов для mapkit >= 20210809.
"Новый слой" RoadEventsLayer пока практически не принимает трафика.

Web clients - in progress.

## General information
| Key | Value |
|---|---|
| ABC | [maps-core-road-events-renderer](https://abc.yandex-team.ru/services/maps-core-road-events-renderer/) |
| Ответственные разработчики | [maps-core-road-events-renderer](https://abc.yandex-team.ru/services/maps-core-road-events-renderer/?scope=development), в первую очередь [Игорь Ретинский](https://staff.yandex-team.ru/retinskii), [Александр Наплавков](https://staff.yandex-team.ru/twisterok) |
| Отвественные SRE | Игорь Ретинский (retinskii@yandex-team.ru) |
| Исходники | [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/road_events/renderer) |
| road events protobuf | [road\_events](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/road_events) |
| vmap2 protobuf | [vmap2](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/renderer/vmap2) |
| Sedem | [sedem\_config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/road_events/renderer/sedem_config) |
| CI | [TestEnv](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_ROAD_EVENTS_RENDERER) |

## Instances
| Environment | URL |
|---|---|
| stable | [maps\_core\_road\_events\_renderer\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_stable/) |
| prestable | [maps\_core\_road\_events\_renderer\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_prestable/) |
| datatesting | [maps\_core\_road\_events\_renderer\_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_datatesting/) |
| testing | [maps\_core\_road\_events\_renderer\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_testing/) |
| load | [maps\_core\_road\_events\_renderer\_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_load/) |
| unstable | [maps\_core\_road\_events\_renderer\_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_unstable/) |


## Graphics
| Key | URL |
|---|---|
| stable (incl. prestable) | [maps-core-road-events-renderer-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-stable-panel-main/) |
| datatesting | [maps-core-road-events-renderer-datatesting-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-datatesting-panel-main/) |
| testing | [maps-core-road-events-renderer-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-testing-panel-main/) |
| load | [maps-core-road-events-renderer-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-load-panel-main/) |
| unstable | [maps-core-road-events-renderer-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-unstable-panel-main/) |
| ratelimiter | [maps_core_road_events_renderer-ratelimiter2-panel](https://yasm.yandex-team.ru/template/panel/maps_core_road_events_renderer-ratelimiter2-panel) |

## Monitorings (Juggler)
| Staging |  URL |
| --- | --- |
| stable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_stable) |
| prestable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_prestable) |
| datatesting | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_datatesting) |
| testing | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_testing) |
| load | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_load) |
| unstable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_road_events_renderer_unstable) |

## Balancers
### L3
| Staging | URL |
|---|---|
| stable external | [core-road-events-renderer.maps.yandex.net](https://l3.tt.yandex-team.ru/service/14036) |
| stable internal | [core-road-events-renderer-internal.maps.yandex.net](https://l3.tt.yandex-team.ru/service/14531) |
| testing | core-road-events-renderer.common.testing.maps.yandex.net |
| datatesting | core-road-events-renderer.common.datatesting.maps.yandex.net |
### L7
| Staging | AWACS | YASM |
|---|---|---|
| stable external | [core-road-events-renderer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-road-events-renderer.maps.yandex.net/show/) | [core-road-events-renderer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-road-events-renderer.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-road-events-renderer-maps;signal=service_total) |
| stable internal | [core-road-events-renderer-internal.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-road-events-renderer-internal.maps.yandex.net/show/) | [core-road-events-renderer-internal.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-road-events-renderer-internal.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-road-events-renderer-maps;signal=service_total) |

## What happens when service is down

Слой (старый и новый) дорожных событий не отображается.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/\* |
| Yacare service | /var/log/yandex/maps/road_events_renderer/road_events_renderer.log\* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/\* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | [YQL](https://yql.yandex-team.ru) : ```SELECT * FROM hahn.`logs/maps-log/1d/{date}` WHERE vhost = 'core-road-events-renderer.maps.yandex.net' limit 1;``` |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

* Убедиться, что в /persitent разделе есть свободное место.
* Убедиться, что create_map отрабатывает корректно и регулярно (примерно раз в минуту): `/var/log/yandex/maps/road_events_renderer/create_map.log`
* Убедиться, что в каталоге `/var/lib/yandex/maps/road_events_renderer/maps/` есть директории вида: `2021.01.01.23.59.59`. Там хранится результат работы create_map
* Убедиться, что ecstatic датасеты активированы /var/lib/yandex/maps/ecstatic/data
* Если при switch-e возник hook failed, то повторяем деплой датасета с помощью команды
    ```sh
        ecstatic reset_errors <ecstatic_dataset_name>=<ecstatic_dataset_version> rtc:maps_core_road_events_renderer_stable
    ```
* Убедиться, что yacare сервис road_events_renderer запущен, при необходимости перезапустить:
    ```sh
        sudo yacare restart road_events_renderer
    ```
* Проверить графики потребления ресурсов [YASM](https://yasm.yandex-team.ru/template/panel/maps-core-road-events-renderer-stable-panel-main/)
    - Cache statistics - Cache hit
    - Cache statistics - Cache usage
    - CPU & Memory %

## Known clients
- Mobile proxy
- Web (TBD)
- JS API (TBD)
- Cartograph (TBD)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_road_events_renderer) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_road_events_renderer.py)

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/lib/yandex/maps/road_events_renderer - там хранится результат работы тулы create_map, который загружает рендерер для создания тайлов
* /logs - логи, сюда ставится симлинка из /var/log

## How to test
### TestApp
Для загрузки TestApp необходим основной yandex аккаунт привязанный к рабочем.  
| Staging | URL (действительны и для iOS) |
|---|---|
| stable | [trunk](https://beta.m.ya.ru/ymta/trunk) |
| testing | [trunk\_testing](https://beta.m.ya.ru/ymta/trunk_testing) |

Тестировать на экранах:
- Старый слой: Road Events
- Новый слой: Road Events 2 & Directions Navigation

Для просмотра ДС из datatesting в TestApp.testing, надо во вкладке Experiments включить switch button 'datatesting'

### HTTP

#### Пример новой ручки
```sh
# get encoded tile
curl --output - -H "Host:core-road-events-renderer.maps.yandex.net" -H 'Accept: application/x-protobuf' '<RENDERER_HOST>/roadevents/tiles?v=2051.01.01.01.01.01&x=163137&y=81375&lang=ru_RU&z=18&zmin=18&zmax=21' > tile.pb

# decode tile
cat tile.pb | ~/arc/arcadia/contrib/tools/protoc/protoc -I ~/arc/arcadia/maps/doc/proto --decode=yandex.maps.proto.common2.response.Response ~/arc/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto > decoded.tile
```

#### Пример старой ручки
```sh
# get decoded vmap2 tile
curl -H 'Accept: text/x-protobuf' 'core-road-events-renderer.common.testing.maps.yandex.net/render?l=accident,drawbridge,police,chat,reconstruction,closed&v=2051.01.01.01.01.01&x=163137&y=81375&lang=ru_RU&z=18&zmin=18&zmax=21'
```

### Стенды

#### БЯК
[production](https://yandex.ru/maps/?l=trf%2Ctrfe)
[datatesting](https://l7test.yandex.ru/maps/?host_config%5Bhosts%5D%5BroadEventsRenderer%5D=https%3A%2F%2Fcore-road-events-renderer.common.testing.maps.yandex.net%2F&host_config%5Binthosts%5D%5BtrfeStamp%5D=http%3A%2F%2Fcore-road-events-renderer.common.testing.maps.yandex.net%2Ftrf%2Fstamp.xml&l=trf%2Ctrfe)
[testing](https://l7test.yandex.ru/maps/?l=trf%2Ctrfe)

#### Картограф
[production](https://cartograph.maps.yandex-team.ru/?service=maps)
[datatesting](https://cartograph.tst.c.maps.yandex-team.ru/?service=maps)

#### JS API
[production](https://pages.github.yandex-team.ru/flapenguin/stands/api.html?api=production)
[testing](https://pages.github.yandex-team.ru/flapenguin/stands/api.html?api=testing)

#### Static API
Static API формирует изображение карты в соответствии со значениями параметров, передаваемых сервису в URL. 
[Пример отображение слоя дорожных событий](https://static-maps.yandex.ru/1.x/?ll=37.620070,55.753630&spn=0.1,0.1&l=map,trfe)
[Подробная документация](https://yandex.ru/dev/maps/staticapi/doc/1.x/dg/concepts/input_params.html)

## Ratelimiter
[ratelimiter](https://abc.yandex-team.ru/services/maps-core-ratelimiter) устанавливает и контролирует лимит на rps сервиса (защита от перегруза), при превышении которого yacare начинает отвечать кодом 429.<br>
[Документация yacare по ratelimiter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare#ratelimiter) и по самому [ratelimiter](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/).<br>
Конфинг ratelimiter'а для road events renderer лежит [здесь](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_road_events_renderer), после мержа изменений в транк новые лимиты начинают действовать примерно через 10 минут (по завершению sandbox задач `MAPS_RATE_PANELS_REFRESHER` и `MAPS_RATE_LIMITS_REFRESHER`, автору комита придет письмо).<br>
[Графики](https://yasm.yandex-team.ru/template/panel/maps_core_road_events_renderer-ratelimiter2-panel).


## API
| Path                  |               | Description                                                           | Client            |
| --------------------- | ------------- | --------------------------------------------------------------------- | ----------------- |
| /roadevents/tiles     |               | Returns road events tiles for new MapKit road events layer implementation. | Mobile proxy |
| Params                | v             | Version of tile                                                       |                   |
|                       | x, y, z       | Tile coordinates                                                      |                   |
|                       | zmin, zmax    | Zoom range for multizoom tiles (ignored for images, default z)        |                   |
|                       | lang          | Tile locale (default en)                                              |                   |
|                       |               |                                                                       |                   |
| /render               |               | Returns road events tiles in vmap2 format. It is used in web clients and old MapKit road events layer implementation. | Mobile proxy |
| Params                | v             | Version of tile                                                       |                   |
|                       | x, y, z       | Tile coordinates                                                      |                   |
|                       | l             | Comma-separated tile layers (e.g. trfe,chat,accident)                 |                   |
|                       | lang          | Tile locale (default rus)                                             |                   |
|                       | vec_protocol  | Protobuf tile format version (ignored for images, default 2)          |                   |
|                       | zmin, zmax    | Zoom range for multizoom tiles (ignored for images, default z)        |                   |
|                       | scale         | Tile image scale factor (ignored for protobuf)                        |                   |
|                       | theme         | Map theme. Values: dark, light (ignored for protobuf, default light)  |                   |
|                       | format        | Tile format. Values: protobuf, png, text                              |                   |
|                       | moderated     | Moderate filter (default all events)                                  |                   |
|                       | experimental_trfe_design | Map design from Cartograph experimental branch             |                   |
|                       |               |                                                                       |                   |
| /tiles                |               | Redirected to /render with png format                                 | StaticAPI         |
|                       |               |                                                                       |                   |
| /1.1/tiles            |               | Redirected to /render with png format                                 | JS API, Web maps  |
| Params                | l             | Comma-separated tile layers. If l=trje is redirected to /hotspots     |                   |
|                       |               |                                                                       |                   |
| /2.x/tiles            |               | Redirected to /render with protobuf format                            | JS API, Web maps  |
|                       |               |                                                                       |                   |
| /hotspots             |               | Returns hotspot tile in json format                                   |                   |
| Params                | v             | Version of tile                                                       |                   |
|                       | x, y, z       | Tile coordinates                                                      |                   |
|                       | l             | Comma-separated tile layers (e.g. trfe,chat,accident)                 |                   |
|                       | locale        | Tile locale                                                           |                   |
|                       | moderated     | Moderate filter (default all events)                                  |                   |
|                       | experimental_trfe_design | Map design from Cartograph experimental branch             |                   |
|                       |               |                                                                       |                   |
| /icons                |               | Returns icon image                                                    | Mobile proxy, JS API, Web maps |
| Params                | scale         | Icon image scale factor                                               |                   |
|                       | id            | Icon id returned in tile                                              |                   |
|                       | c1, c2, c3    | Primary, secondary, tertiary colors to customize icon (optional)      |                   |
|                       |               |                                                                       |                   |
| /glyphs               |               | Returns sdf glyphs in protobuf format                                 | Mobile proxy, JS API, Web maps |
| Params                | font_id       | Font id returned in tile                                              |                   |
|                       | range         | Two comma-separated numbers specify range of glyph ids                |                   |
|                       |               |                                                                       |                   |
| /version              |               | Returns current map version                                           | Mobile proxy      |
| Params                | format        | Content type. Values: protobuf, text, xml                             |                   |
|                       |               |                                                                       |                   |
| /trf/stamp.xml        |               | Redirected to /version with xml format                                | JS API, Web maps  |
|                       |               |                                                                       |                   |

## How to release new soft

Всю информацию по работе с релизами в Sedem Machine [тут](https://docs.yandex-team.ru/sedem/releases)

### Как выкатить в unstable без комита в trunk
* Переходим в папку infopoints `cd ~/arc/arcadia/maps/road_events/renderer/docker`
* Собираем образ и пушим в репозиторий `ya package pkg.json --docker --docker-push --docker-repository=maps` (в случае успеха в выводе команды будет указан тэг нового образа)
* В [Instance Spec](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_road_events_renderer_unstable/instance_spec) указываем тэг образа, собранного на предыдущем этапе
* Сохраняем новый Instance Spec и активируем новый snapshot

Наблюдать за ходом выкладки можно на дашборде из секции [instances](#instances).

## Ecstatic Datasets

| Stable | Testing | Datatesting |
| ------ | ------- | ----------- |
| [yandex-maps-jams-events](http://ecstatic.maps.yandex.net/pkg/yandex-maps-jams-events/versions) | [yandex-maps-jams-events](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-jams-events/versions) | [yandex-maps-jams-events](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-jams-events/versions) |
| [yandex-maps-road-events-design](http://ecstatic.maps.yandex.net/pkg/yandex-maps-road-events-design/versions) | [yandex-maps-road-events-design](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-road-events-design/versions) | [yandex-maps-road-events-design](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-road-events-design/versions) |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-geobase-tzdata](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |


## Firewall macroses
| Staging | URL |
|---|---|
| stable | [`_MAPS_CORE_ROAD_EVENTS_RENDERER_STABLE_RTC_NETS_`](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ROAD_EVENTS_RENDERER_STABLE_RTC_NETS_) |
| testing, load, unstable | [`_MAPS_CORE_ROAD_EVENTS_RENDERER_TESTING_RTC_NETS_`](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ROAD_EVENTS_RENDERER_TESTING_RTC_NETS_) |

## Regression 
[График стрельб в lunapark](https://lunapark.yandex-team.ru/regress/MAPSROADEVENTS?service=maps-core-road-events-renderer)

Как устроены стрельбы можно посмотреть [тут](https://docs.yandex-team.ru/sedem/services/nanny#avtomaticheskoe-nagruzochnoe-testirovanie).<br>
Посмотреть список задач со стрельбами можно по [фильтру](https://sandbox.yandex-team.ru/tasks?children=true&created=14_days&tags=NANNY%3AMAPS_CORE_ROAD_EVENTS_RENDERER_LOAD&type=MAPS_GENERIC_LOAD_TESTING_TASK).<br>
Повторно запустить стрельбу можно на страницес сервиса [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-road-events-renderer%22%7D)
