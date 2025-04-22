# Maps-Core-Carparks-Renderer-Nearby

Выдаёт тайлы слоя парковок вблизи запрошенной точки.

## General information

| | |
| --- | --- |
| Кому звонить, если ничего не понятно | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii))<br>Александр Наплавков ([@twisterok](https://staff.yandex-team.ru/twisterok))|
| Отвественные SRE | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii)) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/renderer |
| Sedem | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/sedem/common/sedem_config |
| | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/sedem/nearby/sedem_config |
| Docker | https://a.yandex-team.ru/arc/trunk/arcadia/maps/carparks/docker/renderer/nearby |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-carparks-renderer-nearby/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_CARPARKS_RENDERER_NEARBY | 

### ratelimiter

Смотри [документацию для renderer-lots](renderer-lots.md#ratelimiter).<br>
Конфинг ratelimiter'а для maps_core_carparks_renderer_nearby лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_carparks_renderer_nearby)<br>

## Instances (Nanny)

| Staging | URL |
| --- | --- |
| *Dashboard*     | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_carparks_renderer_nearby/     |
| testing         | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_testing/        |
| load            | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_load/           |
| datatesting     | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_datatesting/    |
| datavalidation  | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_datavalidation/ |
| prestable       | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_prestable/      |
| stable          | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_carparks_renderer_nearby_stable/         |

## Documentation

Смотри [документацию для renderer-lots](renderer-lots.md#documentation).

Отличие только в том, что используется пешеходный граф, на котором фильтруются отдаваемые геометрические примитивы по расстоянию (параметр `distance`) до некторой точки (параметр `sll`).

### How to release new soft
[Документация про релизы](https://docs.yandex-team.ru/sedem/releases)

## Known clients

* Mobile proxy (МЯК и Навигатор обращаются к прокси через MapKit)
  * Для тестирования используется раздел Carparks (long-tap для выбора области nearby) в TestApp, сборки окружений testing, datatesting, production
* Клиентские браузеры (БЯК)
  * [production](https://maps.yandex.ru)
  * [testing](https://l7test.yandex.ru/maps)

## Ecstatic datasets

* yandex-maps-carparks-layer
* yandex-maps-pedestrian-graph-fb

## What happens when service is down

В Навигаторе исчезнет отображение парковок рядом с адресом или Организацией.
Деградации не предусмотрены.

## How to fix common problems

Смотри [документацию для renderer-lots](renderer-lots.md#how-to-fix-common-problems).

## Балансеры

### AWACS L3-балансер

| Key | Values |
| --- | --- |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-carparks-renderer-nearby.maps.yandex.net/l3-balancers/list/ |
| l3manager | https://l3.tt.yandex-team.ru/service/2069 |
| racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=4755 |

### AWACS L7-балансеры

| Key | Values |
| --- | --- |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-carparks-renderer-nearby.maps.yandex.net/show/ |
| Сервисы Nanny | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-nearby_maps_yandex_net_man/ |
|  | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-nearby_maps_yandex_net_sas/ |
|  | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-carparks-renderer-nearby_maps_yandex_net_vla/ |
| Кофигурация | https://a.yandex-team.ru/arc/trunk/arcadia/infra/awacs/templates/core-carparks-renderer-nearby.maps.yandex.net |
| Графики (common) | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-carparks-renderer-nearby.maps.yandex.net;prj=carparks-nearby;ctype=prod;timelines=0.03,0.05,0.07,0.1,0.3,1,5,10/ |
| Графики (portoinst) | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-carparks-renderer-nearby.maps.yandex.net;prj=carparks-nearby;ctype=prod/ |


- Настройки файрвола: https://puncher.yandex-team.ru/?destination=core-carparks-renderer-nearby.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Мониторинг балансеров: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dcore-carparks-renderer-nearby.maps.yandex.net

## Persistent Volumes

Смотри [документацию для renderer-lots](renderer-lots.md).

## Мониторинги (Juggler)

| Staging         | URL |
| -----------     | --- |
| testing         | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_testing        |
| load            | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_load           |
| datatesting     | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_datatesting    |
| datavalidation  | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_datavalidation |
| prestable       | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_prestable      |
| stable          | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_carparks_renderer_nearby_stable         |

## Графики (Golovan)

| Staging         | URL |
| -----------     | --- |
| testing         | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-testing-panel-main/         |
| load            | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-load-panel-main/            |
| datatesting     | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-datatesting-panel-main/     |
| datavalidation  | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-datavalidation-panel-main/  |
| prestable       | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-prestable-panel-main/       |
| stable          | https://yasm.yandex-team.ru/template/panel/maps-core-carparks-renderer-nearby-stable-panel-main/          |
| ratelimiter     | https://yasm.yandex-team.ru/template/panel/maps_core_carparks_renderer_nearby-ratelimiter2-panel          |

## SLA

[Report in stat](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_carparks_renderer_nearby?scale=d&_incl_fields=d1&_incl_fields=d30&_incl_fields=d7&_incl_fields=n1&_incl_fields=n30&_incl_fields=n7&_period_distance=30)

## Logs

В сервисах Няни, внутри контейнеров, файловые логи можно найти тут: 

| Name | URL/path |
| --- | --- |
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Carparks | /var/log/yandex/maps/carparks-renderer-lots/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Juggler | /juggler/log/* |
| YT | ```SELECT * FROM hahn.`//logs/maps-log/1d/{date}` WHERE vhost = 'core-carparks-renderer-nearby.maps.yandex.net' LIMIT 100;``` |

## Regression Load Testing Configurations

[График стрельб в lunapark](https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-core-carparks-renderer-nearby)

Как устроены стрельбы можно посмотреть [тут](https://docs.yandex-team.ru/sedem/services/nanny#avtomaticheskoe-nagruzochnoe-testirovanie).<br>
Посмотреть список задач со стрельбами можно по [фильтру](https://sandbox.yandex-team.ru/tasks?children=true&created=14_days&tags=NANNY%3AMAPS_CORE_CARPARKS_RENDERER_NEARBY_LOAD&type=MAPS_GENERIC_LOAD_TESTING_TASK).<br>
Повторно запустить стрельбу можно на страницес сервиса [SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-carparks-renderer-nearby%22%7D).<br>
