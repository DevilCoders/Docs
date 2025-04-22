# JSAPI v1.1

[![production version](https://badger.yandex-team.ru/qloud/maps/front-jsapi-v1-1/production/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-jsapi-v1-1/production) [![testing version](https://badger.yandex-team.ru/qloud/maps/front-jsapi-v1-1/testing/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-jsapi-v1-1/testing)

Yandex Maps JavaScript API version 1.1

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-jsapi-v1-1 |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-jsapi-v1-1 |
| TestPalm | https://testpalm2.yandex-team.ru/maps-js-api-v1-x |

## Instances

| Environment | URL | JS API Proxy URL |
|---|---|---|
| Testing | http://jsapi-v1-1.tst.c.maps.yandex.net | https://api-maps.tst.c.maps.yandex.ru/1.1/ |
| Production | | https://api-maps.yandex.ru/1.1/ |

## Documentation

https://tech.yandex.ru/maps/doc/jsapi/1.x/dg/concepts/About-docpage/

## What happens when service is down

A lot of services which show Yandex Maps via JS API 1.1 will be affected (> 40000 websites).

## Monitorings

| Type | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-jsapi-v1-1-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-jsapi-v1-1_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-jsapi-v1-1_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stage/maps-front-jsapi-v1-1_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-jsapi-v1-1_app"` |


## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
