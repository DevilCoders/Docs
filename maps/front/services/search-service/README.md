# search-service [![build status](https://badger.yandex-team.ru/github/maps/search-service/master/state.svg)](https://github.yandex-team.ru/maps/search-service/commits/master)

Proxy to [geosearch](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo) for Yandex Maps JS API.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-search-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-search-service/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://api-maps.tst.c.maps.yandex.ru/services/search/ |
| Production | https://api-maps.yandex.ru/services/search/ |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Known clients

* [jsapi-v2][jsapi-v2]

[jsapi-v2]: https://github.yandex-team.ru/mapsapi/jsapi-v2

## What happens when service is down

* Search and routing by address in [jsapi-v2][jsapi-v2] will stop working.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-search-service_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-search-service_production |

## Backend dashboards

| Name | URL |
|---|---|
| search | https://yasm.yandex-team.ru/template/panel/addrs_kpi |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stages/maps-front-search-service_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-search-service_app"` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-search-service |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Links

Previous version on xscript: https://github.yandex-team.ru/mapsapi/jsapi-services/tree/master/search

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
