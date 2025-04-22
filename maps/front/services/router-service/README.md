# router-service [![build status](https://badger.yandex-team.ru/github/maps/router-service/master/state.svg)](https://github.yandex-team.ru/maps/router-service/commits/master)

Router service for Yandex Maps JS API.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-router-service |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-router-service |

## Instances

| Environment | JS API Proxy URL |
|---|---|
| Testing | http://api-maps.tst.c.maps.yandex.ru/services/route/ |
| Production | https://api-maps.yandex.ru/services/route/ |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Known clients

* [jsapi-v2.1][jsapi-v2.1]
* [jsapi-v2.0][jsapi-v2.0]
* [map-frame-api][map-frame-api]
* [inception-service][inception-service]
* [BiTaxi][BiTaxi]

[jsapi-v2.1]: https://github.yandex-team.ru/maps/jsapi-v2.1
[jsapi-v2.0]: https://github.yandex-team.ru/maps/jsapi-v2.0
[map-frame-api]: https://github.yandex-team.ru/maps/map-frame-api
[inception-service]: https://github.yandex-team.ru/maps/inception-service
[BiTaxi]: http://www.bitaksi.com/en/

## What happens when service is down

* [jsapi-v2.1][jsapi-v2.1]:
  * Will stop to build routes.
  * Will stop to show transport stops info by click on POI.
  * Will stop to show nearest stations info by click on train stations.
* [jsapi-v2.0][jsapi-v2.0]: Will stop to build routes.
* [map-frame-api][map-frame-api]: Will stop to to build routes and show transport stops info.
* [inception-service][inception-service]: Will stop to build routes.
* [BiTaxi][BiTaxi]: Will stop to show route statistic in mobile app (see https://st.yandex-team.ru/MAPSHTTPAPI-398).

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-router-service_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-router-service_production |
| By endpoints | https://yasm.yandex-team.ru/template/panel/maps-front-common/graphs=driving-router,masstransit-router,pedestrian-router,bicycle-router,masstransit-stop,stat-v1;full_env_name=maps-front-router-service_production;mode=full |

## Backend dashboards

| Name | URL |
|---|---|
| apikeys-int | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-apikeys-int.production |
| driving router | https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-stable-panel-main/ |
| masstransit router | https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-stable-panel-main/ |
| bicycle router | https://yasm.yandex-team.ru/template/panel/maps-core-bicycle-router-stable-panel-main/ |
| routers ratelimiter | https://yasm.yandex-team.ru/panel/_31wVgl |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "front-router-service_app"` |

## Regression Stress Testing Configurations

[Stress results](https://st.yandex-team.ru/MAPSHTTPAPI-223)

## Vault

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
