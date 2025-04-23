# coverage-service [![build status](https://badger.yandex-team.ru/github/maps/coverage-service/master/state.svg)](https://github.yandex-team.ru/maps/coverage-service/commits/master)

Provides information about layers.

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-coverage-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-coverage-service |

## Instances

| Environment | URL | Proxy URL |
|---|---|---|
| Testing | http://coverage-service.tst.c.maps.yandex.net/ | https://api-maps.tst.c.maps.yandex.ru/services/coverage/ |
| Production | | https://api-maps.yandex.ru/services/coverage/ |

## Documentation

API method documentation in [swagger](http://swagger.io/specification/) format can be found in
[docs](docs) directory.

## Known clients

* [jsapi-v2][jsapi-v2]

[jsapi-v2]: https://github.yandex-team.ru/mapsapi/jsapi-v2

## What happens when service is down

* [jsapi-v2][jsapi-v2] stops showing tiles and layers (e.g. traffic) in browser.

## How to fix common problems

This service depends from [mapmeta](https://wiki.yandex-team.ru/maps/dev/core/servants/mapmeta/)
backend. If `mapmeta` is unavailable, service will respond with `500` HTTP status code. In this
case check network access to `mapmeta` service.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-coverage-service_production.app |
| Golovan (aka Yasm) | https://yasm.yandex-team.ru/template/alert/maps-front-coverage-service-production-app |

## Dashboards

| Environemnt name | URL |
|---|---|
| Testing | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-coverage-service_testing/ |
| Stress | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-coverage-service_stress/ |
| Production | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-coverage-service_production/ |

## Backend dashboards

| Name | URL |
|---|---|
| mapmeta | https://yasm.yandex-team.ru/panel/maps_core_meta_stable |

## Logs

| Name | URL/path |
|---|---|
| Deploy | https://deploy.yandex-team.ru/stages/maps-front-coverage-service_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-coverage-service_app"` |

## Regression Stress Testing Configurations

| Type | Url |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-coverage-service |
| CI | https://sandbox.yandex-team.ru/scheduler/12185/tasks |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Links

Previous version on [xscript](https://doc.yandex-team.ru/XScript5/interface-developer-guide/concepts/about.xml): https://github.yandex-team.ru/mapsapi/jsapi-services/tree/master/coverage
