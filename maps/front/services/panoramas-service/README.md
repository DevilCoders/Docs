# Panoramas Service

[![production version](https://badger.yandex-team.ru/qloud/maps/front-panoramas-service/production/app/env-version.svg)](https://deploy.yandex-team.ru/stages/maps-front-panoramas-service_production) [![testing version](https://badger.yandex-team.ru/qloud/maps/front-panoramas-service/testing/app/env-version.svg)](https://deploy.yandex-team.ru/stages/maps-front-panoramas-service_testing)

Returns panoramas information by coordinates or oid.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-panoramas-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-panoramas-service |

## Instances

| Environment | JS API Proxy URL |
|---|---|
| Testing | http://api-maps.tst.c.maps.yandex.ru/services/panoramas/ |
| Testing | http://api-maps.tst.c.maps.yandex.ru/panorama/ |
| Production | https://api-maps.yandex.ru/services/panoramas/ |
| Production | https://api-maps.yandex.ru/panorama/ |

### Parameters
See [spec](docs/spec.yaml)

### Supported formats
* `json`

### Examples
Search panorama by coordinates `ll`. <br/>
http://api-maps.yandex.ru/panorama/1.x/?lang=ru_RU&l=stv&ll=28.95034593,41.02815381&spn=0.00127%2C0.00127&format=json

Search panorama by `oid` and `provider`. <br/>
http://api-maps.yandex.ru/panorama/1.x/?lang=ru_RU&l=stv&provider=streetview&oid=1246437363_806428303_23_1310989505&format=json

## Known clients
* JS API
* MAPS

## What happens when service is down
Thousands of external sites stop working or work incorrectly. That means a lot of complaints to our support team.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-panoramas-service_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-panoramas-service_production |

## Backend dashboards

| Name | URL |
|---|---|
| core-stvdescr.stable | https://yasm.yandex-team.ru/template/panel/maps-core-stvdescr-stable-panel-main |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` <br/> https://deploy.yandex-team.ru/stages/maps-front-panoramas-service_production/logs |
| Supervisor | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "front-panoramas-service_app"`) |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
