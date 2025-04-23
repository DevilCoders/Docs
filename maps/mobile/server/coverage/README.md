# maps-core-mobile-coverage

Сервис предоставляет информация о пробочном балле (trfl) и скоростных лимитах (gdnc).

## General Information

| Key                                  | Value                                                                                 |
|--------------------------------------|---------------------------------------------------------------------------------------|
| Кому звонить, если ничего не понятно | Евгений Чернов (chereug@yandex-team.ru)  Александр Любицкий (innocent@yandex-team.ru) |
| SRE                                  | Евгений Чернов (chereug@yandex-team.ru)                                               |
| Исходники                            | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/coverage                |
| Сервис в ABC                         | https://abc.yandex-team.ru/services/maps-core-mobile-coverage                         |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_MOBILE_COVERAGE  |

## Instances

| Environment   | URL                                                                                      |
|---------------|------------------------------------------------------------------------------------------|
| **Dashboard** | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps-core-mobile-coverage  |
| Stable        | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_coverage_stable      |
| Prestable     | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_coverage_prestable   |
| Testing       | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_coverage_testing     |
| Load          | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_coverage_load        |

## Balancers

| Environment   | URL                                                                                                        |
|---------------|------------------------------------------------------------------------------------------------------------|
| Stable        | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-coverage.maps.yandex.net/show/         |
| Testing       | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-coverage.testing.maps.yandex.net/show/ |

## Graphics

| Staging    | URL                                                                                           |
|------------|-----------------------------------------------------------------------------------------------|
| Stable     | https://yasm.yandex-team.ru/template/panel/maps-core-mobile-coverage-stable-panel-main        |
| Prestable  | https://yasm.yandex-team.ru/template/panel/maps-core-mobile-coverage-prestable-panel-main     |
| Testing    | https://yasm.yandex-team.ru/template/panel/maps-core-mobile-coverage-testing-panel-main       |

## Logs

| What           | Where                                                                                                         |
|----------------|---------------------------------------------------------------------------------------------------------------|
| Логи сервиса   | /var/log/yandex/maps/mobile_coverage/mobile_coverage.log                                                      |
| nginx          | /var/log/nginx/access-tskv.log                                                                                |
| ecstatic       | /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log                                                        |
| YT             | USE hahn; SELECT * FROM \`logs/maps-log/1d/2019-11-23\` WHERE vhost = 'core-mobile-coverage.maps.yandex.net'; |

## API

|           |                                             |                                                              |
| --------- | ------------------------------------------- | ------------------------------------------------------------ |
| /tile     | Returns single tile at given coordinates    |                                                              |
|           | in protobuf format                          |                                                              |
| Params    | x, y                                        | Tile coordinates                                             |
|           | z                                           | Zoom level (0 for the root tile, 1 otherwise)                |
|           | v                                           | Coverage layer version in format YYYY.MM.DD.HH24             |
|           | l                                           | Coverage layer type: trfl or gdnc                            |
|           |                                             |                                                              |
| /load     | Loads new coverage layer version            |                                                              |
| Params    | v                                           | Coverage layer version in format YYYY.MM.DD.HH24             |
|           | l                                           | Coverage layer type: trfl or gdnc                            |
|           |                                             |                                                              |
| /drop     | Drops coverage layer version                |                                                              |
| Params    | v                                           | Coverage layer version in format YYYY.MM.DD.HH24             |
|           | l                                           | Coverage layer type: trfl or gdnc                            |

## Known Clients
[Maps Core Mobile Proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/proxy/README.md)

## Ecstatic Datasets
* yandex-maps-mobile-coverage-gdnc
* yandex-maps-mobile-coverage-trfl

## Firewall Macros
| Staging       | URL      |
|---------------|----------|
| Stable  | [\_MAPS_CORE_MOBILE_COVERAGE_STABLE_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_COVERAGE_STABLE_RTC_NETS_) |
| Testing | [\_MAPS_CORE_MOBILE_COVERAGE_TESTING_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_COVERAGE_TESTING_RTC_NETS_) |

## What Happens When Service Is Down
* Исчезают данные о скоростных ограничениях (GDNC)
* Исчезают данные о балле пробок (TRFL)

## How to Fix Common Problems
* Проверить, что правильно раскатились датасеты с версией YYYY.MM.DD.HH24:
  * yandex-maps-mobile-coverage-gdnc, yandex-maps-mobile-init-gdnc
  * yandex-maps-mobile-coverage-trfl, yandex-maps-mobile-init-trfl
* Проверить, что сервис mobile-init отдаёт версию YYYY.MM.DD.HH24
* Проверить, что сервис coverage отдаёт тайлы с версией YYYY.MM.DD.HH24
* Проверить логи сервиса: `tail -f /var/log/yandex/maps/mobile-coverage/mobile-coverage.log`

В целом, важно чтобы mobile-init отдавал одну из версий, развернутых на mobile-coverage.

## Monitorings

| Staging    | URL      |
|------------|----------|
| Stable     | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_coverage_stable&limit=60&view=tiles        |
| Prestable  | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_coverage_prestable&limit=60&view=tiles     |
| Testing    | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_coverage_testing&limit=60&view=tiles       |


## SLA
[Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_mobile_coverage) <br>
[maps_core_mobile_init.py config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_mobile_coverage.py)

## Regression Load Testing Configuration

| Type     | URL |
|----------|-----|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=maps-core-mobile-coverage |
| Ammo     | https://sandbox.yandex-team.ru/scheduler/714416                                    |
| CI       | https://sandbox.yandex-team.ru/scheduler/18574                                     |
