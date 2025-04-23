# Maps-Core-Carparks-Renderer-Lots

Выдаёт тайлы слоя парковок.

## General information

|  |  |
| --- | --- |
| Кому звонить, если ничего не понятно | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii))<br>Александр Наплавков ([@twisterok](https://staff.yandex-team.ru/twisterok))|
| Отвественные SRE | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii)) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/renderer |
| Sedem | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/sedem/common/sedem_config |
| | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/sedem/lots/sedem_config |
| Docker | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/docker/renderer/lots |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-carparks-renderer-lots/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_CARPARKS_RENDERER_LOTS |

## Instances (Nanny)

| Staging | URL |
| --- | --- |
| *Dashboard*             | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_carparks_renderer_lots/             |
| testing                 | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_testing/                |
| load                    | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_load/                   |
| datatesting             | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_datatesting/            |
| datavalidation          | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_datavalidation/         |
| datatestingvalidation   | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_datatestingvalidation/  |
| prestable               | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_prestable/              |
| stable                  | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_lots_stable/                 |

## Documentation

Сервис имеет одновременно несколько версий слоя карты - ровно столько, сколько было билдов слоя в Огороде.
Только одна из версий является активной и включена как дефолтная в продакшене. Активация делается в Огороде.

В сервисе используется кастомный renderer Datasource, который берёт геометрии из .geometry/.index файлов, а также информацию о парковках из .mms файла из датасета.
Datasource налету парсит выражения из дизайна слоя (expression evaluator), находит нужные геометрии в указанном bounding box и выдаёт примитивы для дальнейшего рендеринга тайла библиотекой рендерера.

### ratelimiter

[ratelimiter](https://abc.yandex-team.ru/services/maps-core-ratelimiter) устанавливает и контролирует лимит на rps сервиса (защита от перегруза), при превышении которого yacare начинает отвечать кодом 429.<br>
[Документация yacare по ratelimiter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare#ratelimiter) и по самому [ratelimiter](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/).<br>
Конфинг ratelimiter'а для maps_core_carparks_renderer_lots лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_carparks_renderer_lots), после мержа изменений в транк новые лимиты начинают действовать примерно через 10 минут (по завершению sandbox задач `MAPS_RATE_PANELS_REFRESHER` и `MAPS_RATE_LIMITS_REFRESHER`, автору комита придет письмо).<br>

### Основные ручки

| Ручка | Описание |
| --- | --- |
| /tiles | Рендерит векторный тайл, используется мобильными клиентами |
| /icons | Возвращает иконку по id, нужно для векторных тайлов |
| /maps-rdr-carparks/tiles | Рендерит растровый тайл, используется в БЯК |
| /version | Возвращает активированную версию слоя |
| /renderer?action=open<br>/renderer?action=close | Открывает или закрывает определённую версию слоя, вызываются по ecstatic-хукам |

### Примеры запросов тайла
- растровый тайл:

`curl 'core-carparks-renderer-lots.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&x=39617&y=20540&z=16&lang=ru_RU' > tile.png`

или

`curl -H 'Host: core-carparks-renderer-lots.maps.yandex.net' 'cwh7ozh3pr5wsszw.sas.yp-c.yandex.net/maps-rdr-carparks/tiles?l=carparks&x=39617&y=20540&z=16&lang=ru_RU' > tile.png`
- protobuf тайл:

`curl 'core-carparks-renderer-lots.maps.yandex.net/tiles?l=carparks&x=39617&y=20540&z=16&lang=ru_RU&version=2' > tile.pb.z`

или

`curl -H 'Host: core-carparks-renderer-lots.maps.yandex.net' 'cwh7ozh3pr5wsszw.sas.yp-c.yandex.net/tiles?l=carparks&x=39617&y=20540&z=16&lang=ru_RU&version=2' > tile.pb.z`

через коммунальный балансер 

`curl 'core-carparks-renderer-lots.common.testing.maps.yandex.net/tiles?l=carparks&x=39617&y=20540&z=16&lang=ru_RU&version=2' > tile.pb.z`

Если нужен дизайн Навика, тогда l=vnavparks2.

### Декодирование тайла
```
cat tile.pb.z | perl -MCompress::Zlib -e 'undef $/; print uncompress(<>)' > tile.pb
cat tile.pb | ~/arc/arcadia/contrib/tools/protoc/protoc -I ~/arc/arcadia/maps/doc/proto --decode=yandex.maps.proto.renderer.vmap2.Tile ~/arc/arcadia/maps/doc/proto/yandex/maps/proto/renderer/vmap2/tile.proto
```

### Split View
4-way split view для stable, datavalidation, datatesting, datatestingvalidation и двух вариантов дизайна.

* [Default maps design (МЯК, БЯК, ...)](https://pages.github.yandex-team.ru/avlasyuk/split_view/index.html#55.760237817162334,37.61739545115217!z=16!num_splits=4!title_0=stable!title_1=datavalidation!title_2=datatesting!title_3=datatestingvalidation!url_0=http://core-carparks-renderer-lots.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_1=http://core-carparks-renderer-lots.common.datavalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_2=http://core-carparks-renderer-lots.common.datatesting.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_3=http://carparks-lots.common.datatestingvalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_0=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_1=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_2=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_3=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU)
* [Navi design](https://pages.github.yandex-team.ru/avlasyuk/split_view/index.html#55.760237817162334,37.61739545115217!z=16!num_splits=4!title_0=stable!title_1=datavalidation!title_2=datatesting!title_3=datatestingvalidation!url_0=http://core-carparks-renderer-lots.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_1=http://core-carparks-renderer-lots.common.datavalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_2=http://core-carparks-renderer-lots.common.datatesting.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_3=http://carparks-lots.common.datatestingvalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_0=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_1=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_2=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_3=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU)
* [Default vs Navi design (stable, datavalidation)](https://pages.github.yandex-team.ru/avlasyuk/split_view/index.html#55.760237817162334,37.61739545115217!z=16!num_splits=4!title_0=Default%20design%20stable!title_1=Navi%20design%20stable!title_2=Default%20design%20datavalidation!title_3=Navi%20design%20datavalidation!url_0=http://core-carparks-renderer-lots.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_1=http://core-carparks-renderer-lots.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_2=http://core-carparks-renderer-lots.common.datavalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_3=http://core-carparks-renderer-lots.common.datavalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_0=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_1=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_2=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_3=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU)
* [Default vs Navi design (datatesting, datatestingvalidation)](https://pages.github.yandex-team.ru/avlasyuk/split_view/index.html#55.760237817162334,37.61739545115217!z=16!num_splits=4!title_0=Default%20design%20datatesting!title_1=Navi%20design%20datatesting!title_2=Default%20design%20datatestingvalidation!title_3=Navi%20design%20datatestingvalidation!url_0=http://core-carparks-renderer-lots.common.datatesting.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_1=http://core-carparks-renderer-lots.common.datatesting.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_2=http://carparks-lots.common.datatestingvalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=carparks&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!url_3=http://carparks-lots.common.datatestingvalidation.maps.yandex.net/maps-rdr-carparks/tiles?l=vnavparks2&version=2&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_0=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_1=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_2=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU!bg_url_3=https://core-renderer-tiles.maps.yandex.net/tiles?l=map&x=%25x&y=%25y&z=%25z&lang=ru_RU)

### How to release new soft
[Документация про релизы](https://docs.yandex-team.ru/sedem/releases)

## Known clients

* Mobile proxy (МЯК и Навигатор обращаются к прокси через MapKit)
  * Для тестирования используется раздел Carparks в TestApp, сборки окружений testing, datatesting, production
  * Для просмотра данных из datatesting, datavalidation и datatestingvalidation надо в TestApp, во вкладке Experiments добавить:
    ```
      Service ID MAPS_CONFIG
      Parameter name experimental_datatesting (experimental_datavalidation)
      Parameter value 1

      или

      Service ID RENDERER
      Parameter name experimental_datatestingvalidation
      Parameter value 1

    ```
* Клиентские браузеры (БЯК)
  * [production](https://maps.yandex.ru)
  * [testing](https://l7test.yandex.ru/maps)
  * [datatesting](https://l7test.yandex.ru/maps?l=carparks&host_config[inthosts][carparksStamp]=http%3A%2F%2Fcore-carparks-renderer-lots.common.testing.maps.yandex.net%2Fmaps-rdr-carparks%2Fstamp.xml%3Fexperimental_datatesting%3D1&renderer_experimental_datatesting=1)
  * [datavalidation](https://l7test.yandex.ru/maps?l=carparks&host_config[inthosts][carparksStamp]=http%3A%2F%2Fcore-carparks-renderer-lots.common.testing.maps.yandex.net%2Fmaps-rdr-carparks%2Fstamp.xml%3Fexperimental_datavalidation%3D1&renderer_experimental_datavalidation=1)
  * [datatestingvalidation](https://l7test.yandex.ru/maps?l=carparks&host_config[inthosts][carparksStamp]=http%3A%2F%2Fcore-carparks-renderer-lots.common.testing.maps.yandex.net%2Fmaps-rdr-carparks%2Fstamp.xml%3Fexperimental_datatestingvalidation%3D1&renderer_experimental_datatestingvalidation=1)

## Ecstatic datasets

* yandex-maps-carparks-layer

## What happens when service is down

В БЯК, МЯК и Навигаторе исчезнет отображение парковок.
Деградации не предусмотрены.

## How to fix common problems

* Проверить, что билд Carparks в [Огороде](https://garden.maps.yandex-team.ru/carparks) прошёл успешно и успешно [активировался](https://garden.maps.yandex-team.ru/carparks_activation).
* Проверить логи `ecstatic-agent.log` и `carparks-renderer-lots-hooks.log` и убедиться, что новая версия слоя нормально открыта рендерером и активировалась.
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

### AWACS L3-балансер

| Key | Values |
| --- | --- |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-carparks-renderer-lots.maps.yandex.net/l3-balancers/list/ |
| l3manager | https://l3.tt.yandex-team.ru/service/2139 |
| racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=4804 |

### AWACS L7-балансеры

| Key | Values |
| --- | --- |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-carparks-renderer-lots.maps.yandex.net/show/ |
| Сервисы Nanny | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-lots_maps_yandex_net_man/ |
|  | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-lots_maps_yandex_net_sas/ |
|  | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-lots_maps_yandex_net_vla/ |
| Кофигурация | https://a.yandex-team.ru/arc/trunk/arcadia/infra/awacs/templates/core-carparks-renderer-lots.maps.yandex.net |
| Графики (common) | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-carparks-renderer-lots.maps.yandex.net;prj=carparks-lots;ctype=prod;timelines=0.03,0.05,0.07,0.1,0.3,1,5,10/ |
| Графики (portoinst) | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-carparks-renderer-lots.maps.yandex.net;prj=carparks-lots;ctype=prod/ |


- Настройки файрвола: https://puncher.yandex-team.ru/?destination=core-carparks-renderer-lots.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Мониторинг балансеров: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dcore-carparks-renderer-lots.maps.yandex.net

## Persistent Volumes

- `/logs`
- `/var/lib/yandex/maps/carparks`
- `/var/lib/yandex/maps/ecstatic`
- `/var/www/layers-mobile/carparks` - статические файлы для ручки /version и /stamp.xml

## Мониторинги (Juggler)

| Staging               | URL |
| --------------------- | --- |
| testing               | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_testing                |
| load                  | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_load                   |
| datatesting           | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_datatesting            |
| datavalidation        | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_datavalidation         |
| datatestingvalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_datatestingvalidation  |
| prestable             | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_prestable              |
| stable                | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_lots_stable                 |

## Графики (Golovan)

| Staging               | URL |
| --------------------- | --- |
| testing               | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-testing-panel-main/               |
| load                  | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-load-panel-main/                  |
| datatesting           | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-datatesting-panel-main/           |
| datavalidation        | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-datavalidation-panel-main/        |
| datatestingvalidation | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-datatestingvalidation-panel-main/ |
| prestable             | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-prestable-panel-main/             |
| stable                | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-lots-stable-panel-main/                |
| ratelimiter           | https://yasm.yandex-team.ru/template/panel/maps_core_carparks_renderer_lots-ratelimiter2-panel/               |

## SLA

[Report in stat](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_carparks_renderer_lots?scale=d&_incl_fields=d1&_incl_fields=d30&_incl_fields=d7&_incl_fields=n1&_incl_fields=n30&_incl_fields=n7&_period_distance=30)

## Logs

| Name | URL/path |
| --- | --- |
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Carparks | /var/log/yandex/maps/carparks-renderer-lots/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Juggler | /juggler/log/* |
| YT | ```SELECT * FROM hahn.`//logs/maps-log/1d/{date}` WHERE vhost = 'core-carparks-renderer-lots.maps.yandex.net' LIMIT 100;``` |

## Regression Load Testing Configurations

[График стрельб в lunapark](https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-carparks-renderer-lots)

Как устроены стрельбы можно посмотреть [тут](https://docs.yandex-team.ru/sedem/services/nanny#avtomaticheskoe-nagruzochnoe-testirovanie).<br>
Посмотреть список задач со стрельбами можно по [фильтру](https://sandbox.yandex-team.ru/tasks?children=true&created=14_days&tags=NANNY%3AMAPS_CORE_CARPARKS_RENDERER_LOTS_LOAD&type=MAPS_GENERIC_LOAD_TESTING_TASK).<br>
Повторно запустить стрельбу можно на страницес сервиса [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-carparks-renderer-lots%22%7D).<br>
