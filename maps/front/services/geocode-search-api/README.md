# geocode-search-api

There are several HTTP API in this application:

* [geocoder-api](https://tech.yandex.com/maps/geocoder/)
* [search-api](https://tech.yandex.com/maps/geosearch/)

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-geocode-search-api |
| CI | https://sandbox.yandex-team.ru/tasks?desc_re=maps%2Fgeocode-search-api&owner=MAPS_FRONT |
| Deploy | https://yd.yandex-team.ru/projects/maps-front-geocode-search-api |
| Awacs | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-geocode-search-api.slb.maps.yandex.net/ |
| RPS Limiter | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-geocode-search-api/editor |

## Instances

### search-api
| Environment | URL |
|---|---|
| Testing | https://search-api.tst.c.maps.yandex.net/ |
| Production | https://search-maps.yandex.ru/ |

### geocode-api
| Environment | URL |
|---|---|
| Testing | https://geocode-api.tst.c.maps.yandex.net/ |
| Production | https://geocode-maps.yandex.ru/ |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

**Note**. There is not classic traffic routing because one component handles traffic for different APIs. The codebase for all this APIs is similar; so, that's why they are combined to one service.

Two extra environments are created for `testing` and `production` to route all this traffic properly. Here how it works for `production` (it's absolutely the same for `testing` environment).
```
geocode-maps.yandex.ru -> production-geocode -> production
search-maps.yandex.ru -> production-search -> production
```

## Known clients

* Internal clients
* External clients
* Enterprise clients

**Important note.** When IP of `geocode-search-api` balancers is changed, all external paid clients and our support team must be notified. Usually web-server (e.g nginx) caches IPs; so, web-server should be reloaded to get updated IP.


## What happens when service is down

* Services of internal, external and enterprise clients are degradaded.

## Controlling DC load balancing

In case of an incident in a certain data center, traffic should be redirected to other DCs.
This service uses two-level balancer configuration and that means that redirecting traffic can only be safely achieved by changing the DC traffic ratio.
You can change DC traffic ratio by [ITS](https://wiki.yandex-team.ru/runtime-cloud/nanny/its/):

- [front-geocode-search-api.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/l7heavy/front-geocode-search-api.slb.maps.yandex.net/)

After changing press "_Save sections weight_" and then "_Push to ITS_".

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-geocode-search-api_production.app |
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-geocode-search-api-production-app |

## Dashboards

| Name | URL |
|---|---|
| Main | [YASM](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-geocode-search-api_production;graphs=geocode-api,search-api/) |

## Backend dashboards

| Name | URL |
|---|---|
| `apikeys-int` |  https://github.yandex-team.ru/maps/apikeys-int#dashboards |
| `geosearch` |  https://yasm.yandex-team.ru/template/panel/addrs_kpi |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` |
| Nginx | `/var/log/nginx/access-tskv.log` |
| Deploy logs | https://yd.yandex-team.ru/stage/maps-front-geocode-search-api_production/logs |
| YT | `hahn.[home/logfeller/logs/maps-front-production-log]` |
| YT (geocode-api) | [yql example](https://yql.yandex-team.ru/Operations/XXgbcWim9eQxY4wpQ4QA0QNuicZZlz9o6iI4gK6otLk=) |
| YT (search-api) | [yql example](https://yql.yandex-team.ru/Operations/XXgbCp9LngC4hzTdpzagu8K0WElxsqN7XlgRU0N2ZXk=) |

## Regression Stress Testing Configurations

### search-api
| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-geocode-search-api |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
