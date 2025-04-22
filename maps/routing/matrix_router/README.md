## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Александр Игнатьев [(@asi81)](https://staff.yandex-team.ru/asi81) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Игорь Мартынов [(@immartynov)](https://staff.yandex-team.ru/immartynov) |
| Ответственные SRE | Константин Колганов [(@kmkolganov)](https://staff.yandex-team.ru/kmkolganov) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-matrix-router/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_DRIVING_MATRIX_ROUTER |
| SEDEM panel | [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={"sedem_service":%20"core-driving-matrix-router"}) |
| API | https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/README.md |

## EndPoints

| Environment | URL |
|---|---|
| stable | http://core-driving-matrix-router.maps.yandex.net/ |
| testing | http://core-driving-matrix-router.testing.maps.yandex.net/ |

# <font color='red'>**Как откатывать данные и ПО** </font>
Сначала следует посмотреть на [таймлайн](https://infra.yandex-team.ru/timeline?preset=MwWErEpo2Ln&status=all) и определить причину проблемы.
Далее, с помощью [инструкции](https://wiki.yandex-team.ru/users/shalyga/instrukcija-po-otkatu-dannyx-i-po-matrichnogo-routera), откатить нужный сервис или данные.

## Instances
| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_stable |
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_prestable |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_datatesting |
| datatestingvalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_datatestingvalidation |
| datavalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_datavalidation |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_testing |
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_matrix_router_load |

## Known clients
| Client | TVM id | Network macroses |
|---|---|---|
| B2B Geo| 2011656 | \_B2BGEO_ROUTING_PUBLIC_API_STABLE_NETS\_, \_B2BGEO_YA_COURIER_PROD_NETS\_ |
| Taxi logistic dispatcher | 2020945 | \_HWTAXINETS\_, \_TAXITESTNETS\_ |
| Yandex.Eda | 2019775, 2019773 | \_EDANETS\_, \_EDATESTNETS\_ |
| B2B Geo Analytics | 2021862 | [staff](https://staff.yandex-team.ru/departments/yandex_content_geodev_tech) |

## Graphics
| Type |
|---|
| [stable+prestable](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-stable-panel-main/) |
| [prestable](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-prestable-panel-main/) |
| [datavalidation](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-datavalidation-panel-main/) |
| [datatestingvalidation](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-datatestingvalidation-panel-main/) |
| [datatesting](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-datatesting-panel-main/) |
| [testing](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-testing-panel-main/) |
| [load](https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-matrix-load-panel-main/) |

### Ratelimiter
* [Golovan Ratelimiter panel for stable](https://yasm.yandex-team.ru/template/panel/maps_core_driving_matrix_router-ratelimiter2-panel/)
* [Ratelimiter configs in Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_driving_matrix_router/)

### Monitorings
| Type | URL |
|---|---|
| stable (with prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_stable |
| prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_prestable |
| datavalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_datavalidation |
| datatestingvalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_datatestingvalidation |
| datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_datatesting |
| testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_testing |
| load | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_load |

## Ecstatic datasets
* yandex-maps-graph-speed-profiles
* yandex-maps-jams-closures
* yandex-maps-geodata6
* yandex-maps-geobase-tzdata
* yandex-maps-l6a-matrix-jams-diff-[stable, datatesting, datavalidation, datatestingvalidation, testing]
* yandex-maps-matrix-router-runtime-config

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/spool/yandex/maps/closures/latest - симлинка на последнюю версию closures
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_STABLE_RTC_NETS_\_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_DRIVING_MATRIX_ROUTER_TESTING_RTC_NETS_\_]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_TESTING_RTC_NETS_ ) |
| datavalidation | [_\_MAPS_CORE_DRIVING_MATRIX_ROUTER_DATAVALIDATION_RTC_NETS_\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_DATAVALIDATION_RTC_NETS_ ) |
| datatesting | [_\_MAPS_CORE_DRIVING_MATRIX_ROUTER_DATATESTING_RTC_NETS_\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_MATRIX_ROUTER_DATATESTING_RTC_NETS_ ) |

## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Nginx | /var/log/nginx/* |
| matrix-router | /var/log/yandex/maps/matrix_router/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/maps/roquefort/* |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-09-01` WHERE vhost = 'core-driving-matrix-router.maps.yandex.net' LIMIT 1; |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-matrix-router-log/1d/2021-09-02` WHERE url_path = '/v2/matrix' LIMIT 1; |


### Logbroker

| Environment | Log | Account | Topic | Log on YT |
|---|---|---|---|---|
| stable| /var/log/yandex/maps/matrix_router/matrix_router.log | [maps_matrix_router](https://lb.yandex-team.ru/logbroker/accounts/maps_matrix_router) | [maps-matrix-router-log](https://lb.yandex-team.ru/logbroker/accounts/maps_matrix_router/prod/maps-matrix-router-log) | [//logs/maps-matrix-router-log/1d/](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-matrix-router-log/1d) |


### Метрики качества
https://datalens.yandex-team.ru/3jdjhrje2lpkw-matrixrouterqualitymetrics

## SLA
  * Criteries: https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_driving_matrix_router.py
  * Statbox: https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_driving_matrix_router

## Regression Stress Testing Configurations
* Регрессионные стрельбы по матричному роутеру
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-driving-matrix-router
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/420823
    * Тикет: https://st.yandex-team.ru/MAPSCORE-4875

## MDS
Результат обработки асинхронных запросов загружается в MDS, а клиент получает ссылку на скачивание из MDS

| Environment | bucket project id | Dashboard | Alert |
|---|---|---|---|
| production | matrix-router-result | [MDS space usage](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=matrix-router-result)<br> [MDS proxy statuses](https://yasm.yandex-team.ru/template/panel/mds_proxy/ns=matrix-router-result) | [MDS quota usage](https://juggler.yandex-team.ru/check_details/?host=maps_core_driving_matrix_router_stable&service=mds-disk-quota-perc-usage-matrix-router-result&last=1DAY)<br> [MDS 4xx (prestable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-prestable)<br> [MDS 4xx (stable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-stable)<br> [MDS 5xx (prestable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-prestable)<br> [MDS 5xx (stable)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-stable) |
| testing | matrix-router-result | [MDS space usage](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=matrix-router-result;env=test) | [MDS quota usage](https://juggler.yandex-team.ru/check_details/?host=maps_core_driving_matrix_router_testing&service=mds-disk-quota-perc-usage-matrix-router-result&last=1DAY)<br> [MDS 4xx (testing)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-4xx-testing)<br> [MDS 5xx (testing)](https://yasm.yandex-team.ru/alert/matrix-router-mds-get-5xx-testing) |

## MDB

| Environment | Monitorings |
|---|---|
| stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_stable%26service%3Dmongodb-mdb-* |
| testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_matrix_router_testing%26service%3Dmongodb-mdb-* |

### MDB connection URL
[Смотри в конфиге матричного роутера](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/yacare/lib/config.cpp?rev=r7647602#L123)

### Работа с Mongo DB

По работе с монгой удобный UI: https://nosqlbooster.com/downloads
Создание индекса: 
На автоудаление:
```
db.getCollection("tasks").createIndex({ "creation_timestamp": 1 }, {
    "name": "expire_index",
    "expireAfterSeconds": 604800
})
```

На поиск по токену:
```
db.getCollection("tasks").createIndex({ "token": 1 }, {
    "name": "token_index",
    "background": true
})
```

Удаление индексов:
```
db.tasks.dropIndex("expire_index");
db.tasks.dropIndex("token_index");
```

## Архитектура

### Асинхронные запросы

[Общая идая и описание дублирования асинхронных запросов](https://st.yandex-team.ru/MAPSNAVI-5454#5d9f02b4701665001ddb6d10)

### Примеры запросов

### Запрос на `/calculate`

Запросы принимаются только в бинарных протобафах. Из шелла можно попробовать так:

1. Создать текстовый протобаф.

```
$ cat <<END > text-request
srcll { longitude: 37.588687 latitude: 55.733911 }
srcll { longitude: 37.537786 latitude: 55.796942 }
dstll { longitude: 37.642704 latitude: 55.735345 }
dstll { longitude: 37.534252 latitude: 55.749924 }
departure_time: 1626814121
END
```

2. Закодировать бинарный протобаф с помощью `protoc`.

Находясь в корне аркадии:
```
protoc --proto_path . --encode maps.routing.matrix_router.Request maps/routing/matrix_router/proto/request.proto < text-request > binary-request
```

3. Отправить POST-запрос на ручку `/calculate`.

```
curl -H 'Content-Type: application/x-protobuf' -H 'Accept: text/x-protobuf' --data-binary @binary-request '<router url>/calculate'
```

### Внутренние запросы

`/dev_regions_with_closures` возвращает список регионов с id и именем каждого региона, в котором в данный момент используются перекрытия (а значит, не используются пробки).

## Параметры запросов

#### Внутренние параметры

`debug` включает режим дебага: можно получить геометрию ребер и скорости на ребрах найденных маршрутов. Отрисовать можно с помощью `quality_reporter/draw_routes`. Режим дебага работает медленно.

`disable_scaling` выключает скейлинг --- преобразование ответов.

#### Общие параметры

`disable_jams` выключает использование реалтайм пробочного диффа

`disable_slices` выключает использование исторических диффов 

## Подготовка данных и метрики

#### Подготовка данных
Два раза в неделю обновляются статистические данные:
https://sandbox.yandex-team.ru/scheduler/18487/view

#### Вычисление метрик
Таска на вычисление метрик:
https://sandbox.yandex-team.ru/scheduler/22067/view

#### Валидация метрик
Таска на валидацию метрик:
https://sandbox.yandex-team.ru/scheduler/22273/view

Пороговые значения: https://st.yandex-team.ru/MAPSNAVI-5700

## MapsMatrixRouterShooting

Таска тестирования матричного роутера:
https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsMatrixRouterShootingTask

Планировщик таски тестирования матричного роутера:
https://sandbox.yandex-team.ru/scheduler/43483/tasks?hidden=true&all_tags=false&all_hints=false&limit=20

##Шардирование
https://wiki.yandex-team.ru/users/asi81/shardirovanie-v-matrichnom-routere/
