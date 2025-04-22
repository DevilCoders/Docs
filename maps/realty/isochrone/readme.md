[[toc]]

## About
Сервис Maps Core Realty Isochrone возвращает автомобильные изохроны, то есть полигоны областей, откуда достижима указанная точка (входящий изохрон) или какие точки достижимы из указанной точки (исходящий изохрон) на автомобиле за указанное время.

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Игорь Ретинский (retinskii@yandex-team.ru)<br>Александр Наплавков (twisterok@yandex-team.ru) |
| Отвественные SRE | Игорь Ретинский (retinskii@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/realty/isochrone |
| Sedem | https://a.yandex-team.ru/arc/trunk/arcadia/maps/realty/isochrone/sedem_config |
| Docker | https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/realty/isochrone/docker |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-realty-isochrone/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_REALTY_ISOCHRONE |

## Instances
| Environment | URL |
|---|---|
| **Nanny dashboard** | [maps_core_realty_isochrone](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_realty_isochrone)          |
| Stable              | [maps_core_realty_isochrone_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_realty_isochrone_stable)       |
| Prestable           | [maps_core_realty_isochrone_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_realty_isochrone_prestable) |
| Testing             | [maps_core_realty_isochrone_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_realty_isochrone_testing)     |
| Load                | [maps_core_realty_isochrone_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_realty_isochrone_load)           |

## Graphics dashboards
| Staging | Golovan panel |
|---|---|
| Stable      | [maps-core-realty-isochrone-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-realty-isochrone-stable-panel-main)       |
| Prestable   | [maps-core-realty-isochrone-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-realty-isochrone-prestable-panel-main) |
| Testing     | [maps-core-realty-isochrone-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-realty-isochrone-testing-panel-main)     |
| Load        | [maps-core-realty-isochrone-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-realty-isochrone-load-panel-main)           |
| ratelimiter | [maps_core_realty_isochrone-ratelimiter2-panel](https://yasm.yandex-team.ru/template/panel/maps_core_realty_isochrone-ratelimiter2-panel/)    |

## Monitorings (Juggler)
| Staging |  URL |
| --- | --- |
| stable    | [maps_core_realty_isochrone_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_realty_isochrone_stable)        |
| prestable | [maps_core_realty_isochrone_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_realty_isochrone_prestable)  |
| testing   | [maps_core_realty_isochrone_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_realty_isochrone_testing)      |
| load      | [maps_core_realty_isochrone_load](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_realty_isochrone_load)            |

## What happens when service is down
В сервисе Яндекс.Недвижимость не будет работать поиск объектов по доступности на автомобиле.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/isochrone/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YQL | ``` SELECT * FROM hahn.`//logs/maps-log/1d/{date}` WHERE vhost = 'core-realty-isochrone.maps.yandex.net' LIMIT 100; ``` | 

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Где посмотреть.
Можно посмотреть [изохрон на разработческом стенде](http://maps-mobgeoplatform-dev.vla.yp-c.yandex.net/isochrone.html) (вверху слева ввести адрес объекта)<br>

Можно посмотреть изохрон на сайте Недвижимости (нажать "Время на дорогу").
* [Testing](https://realty.test.vertis.yandex.ru/moskva/kupit/kvartira/karta/)
* [Stable](https://realty.yandex.ru/moskva/kupit/kvartira/karta/)

## Documentation
[Описание изохронов, правда в ОТ](https://wiki.yandex-team.ru/users/allobanov/isochrone/)

[Тикет на автомобильный изохрон](https://st.yandex-team.ru/MAPSNAVI-4980)

На сервис приходит запрос с координатами точки (rll) и указанием времени на дорогу в секундах (timeleft). Сервис возвращает MultiPolygon2, где граница полигона - это точки, откуда можно доехать на машине до исходной точки за указанное время.

Внутри на road_graph применяется алгоритм Дейкстры, мы сохраняем достижимые вершины для каждого шага по времени. Затем для полученного облака точек применяем alpha-shape с условным радиусом hull_radius (тоже можно передать как параметр) и получаем невыпуклую оболочку в виде набора точек. Дальше из неё формируется несколько полигонов.

В качестве пробок используются данные, построенные на базе исторических пробок. Берутся наихудшие пробки для каждого часового пояса между 7 и 11 часами по локальному времени. Пробки доставляются в датасете yandex-maps-realty-jams.

### How to release new soft
[Документация про релизы](https://docs.yandex-team.ru/sedem/releases)

### TVM
Сервис предполагает работу через tvm. Но на время переходного периода
поддерживает работу и без него<br>

Для получения tvm ticket-а нужно воспользоваться tvmknife:
``` sh
# testing
ya tool tvmknife get_service_ticket sshkey -s 2020699 -d 2020699
# production
ya tool tvmknife get_service_ticket sshkey -s 2020701 -d 2020701
```

### API

#### GET /isochrone/

Возвращает автомобильные изохроны.
Может возвращать ответ в формате json или protobuf, в зависимости от переданного хедера ACCEPT:
- application/x-protobuf (`default`), координаты в порядке lon, lat
- text/json, координаты в порядке lat, lon

При возврате protobuf будет отправлен объект GeoObject с заполненой geometry (MultyPoligon)<br>
- [GeoObject](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/geo_object.proto)
- [MultiPolygon](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/geometry.proto?rev=4325596#L49)

Параметры запроса:
| Parameter | Description | Type |
|---|---|---|
| `rll` | lon/lat точка | `required` |
| `timeleft` | Максимальное удаление по времени от заданной точки | `required` |
| `use_jams` | Использование информации о пробках для расчета | default true |
| `hull_radius` | Задает минимальное удаление от предыдущей точки при обходе графа| default берется из config-а |
| `outgoing` | Если `true`, то строится исходящий изохрон, в противном случае - входящий | default=false |


### Пример запроса
Построить 30-минутный изохрон<br>

``` sh
# Через балансер
curl 'core-realty-isochrone.maps.yandex.net/isochrone?rll=37.633396,55.745773&timeleft=1800'

# Без tvm на конкретный хост:
curl -H 'Host: core-realty-isochrone.maps.yandex.net' '<host>/isochrone?rll=37.633396,55.745773&timeleft=1800'

# С использованием tvm на конкретный хост:
curl -H 'X-Ya-Service-Ticket: <tvm-ticket>' -H 'Host: core-realty-isochrone.maps.yandex.net' '<host>/isochrone?rll=37.633396,55.745773&timeleft=1800'
```

Для получения tvm ticket-а см. [TVM](#tvm)

## Known clients
Веб-клиент Яндекс.Недвижимость
Маркет, Еда, Лавка для аналитики и рассчёта областей доставки

## SLA
* [Статистика](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_realty_isochrone)
* [Скрипт](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_realty_isochrone.py)


## Ecstatic Datasets
* yandex-maps-graph-activator
* yandex-maps-graph-compact
* yandex-maps-graph-compact-rtree
* yandex-maps-graph-compact-edges-persistent-index
* yandex-maps-realty-jams

## Балансеры

### AWACS L3-балансер
| Key | Values |
| --- | --- |
| production | [core-realty-isochrone.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-realty-isochrone.maps.yandex.net/) |
| testing | [core-realty-isochrone.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/) |
| l3 manager | https://l3.tt.yandex-team.ru/service/5826 |
| racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=7232 |

### AWACS L7-балансеры

| Key | Values |
| --- | --- |
| L7-балансеры. Сервисы | [rtc_balancer_core-realty-isochrone_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-realty-isochrone_maps_yandex_net_man/)<br>[rtc_balancer_core-realty-isochrone_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-realty-isochrone_maps_yandex_net_sas/)<br>[rtc_balancer_core-realty-isochrone_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-realty-isochrone_maps_yandex_net_vla/) |

## Persistent Volumes
* `/persistent` - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * `/var/lib/yandex/maps/ecstatic` - все данные экстатика
* `/logs` - логи, сюда ставится симлинка из `/var/log`

## Firewall macroses
| Staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_REALTY_ISOCHRONE_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_REALTY_ISOCHRONE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_REALTY_ISOCHRONE_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_REALTY_ISOCHRONE_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
[График стрельб в lunapark](https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=maps-core-realty-isochrone)<br>

Как устроены стрельбы можно посмотреть [тут](https://docs.yandex-team.ru/sedem/services/nanny#avtomaticheskoe-nagruzochnoe-testirovanie).<br>
Посмотреть список задач со стрельбами можно по [фильтру](https://sandbox.yandex-team.ru/tasks?children=true&created=14_days&tags=NANNY%3AMAPS_CORE_REALTY_ISOCHRONE_LOAD&type=MAPS_GENERIC_LOAD_TESTING_TASK).<br>
Повторно запустить стрельбу можно на страницес сервиса [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-realty-isochrone%22%7D)

## Квота sandbox
[MAPS-CORE-AUTO-ISOCHRONE](https://sandbox.yandex-team.ru/admin/groups/MAPS-CORE-AUTO-ISOCHRONE/general)
