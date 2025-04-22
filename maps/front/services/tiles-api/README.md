# tiles-api

Enterprise proxy to [tile renderer](https://wiki.yandex-team.ru/maps/dev/core/layers/).

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-tiles-api |
| CI | https://teamcity.yandex-team.ru/viewType.html?buildTypeId=mapsapi_TilesApi_Master |
| Deploy | https://yd.yandex-team.ru/projects/maps-front-tiles-api |
| Awacs | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-tiles-api.slb.maps.yandex.net/show/ |
| RPS Limiter | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-tiles-api/editor |

## Instances

| Environment | URL |
|---|---|
| Testing | https://tiles-api.tst.c.maps.yandex.net/ ([request example](https://tiles-api.tst.c.maps.yandex.net/v1/tiles?x=19852&y=10154&z=15&lang=ru_RU&l=map&apikey=b027f76e-cc66-f012-4f64-696c7961c395&projection=web_mercator)) |
| Production | https://tiles.api-maps.yandex.ru/ ([request example](https://tiles.api-maps.yandex.ru/v1/tiles/?x=19852&y=10154&z=15&lang=ru_RU&l=map&apikey=55b16091-6e5b-4e78-b438-abd0b8cf8040&projection=web_mercator)) |

## Known clients
Ask [dvshelehov@](https://staff.yandex-team.ru/dvshelehov) for known clients.

## API Documentation
API method documentation in [swagger](http://swagger.io/specification/) format can be found in [docs](docs) directory.

## What happens when service is down
Part of whole applications of all our enterprise clients work incorrectly.

## Controlling DC load balancing

In case of an incident in a certain data center, traffic should be redirected to other DCs.
This service uses two-level balancer configuration and that means that redirecting traffic can only be safely achieved by changing the DC traffic ratio.
You can change DC traffic ratio by [ITS](https://wiki.yandex-team.ru/runtime-cloud/nanny/its/):

- [front-tiles-api.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/l7heavy/front-tiles-api.slb.maps.yandex.net/)

After changing press "_Save sections weight_" and then "_Push to ITS_".

## SLA
99% requests are handled properly.

* Response http code not 5xx.
* Upstream time less than 200 ms.

[SLA Graph](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_front_tiles_api)

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-tiles-api_production.app |

## Dashboards
| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-tiles-api_production |
| Deploy | https://yd.yandex-team.ru/stage/maps-front-tiles-api_production/monitoring |

## Backend dashboards
| Name | URL |
|---|---|
| apikeys-int | https://a.yandex-team.ru/arc_vcs/maps/front/services/apikeys-int#dashboards |
| maps-core-renderer-cache <br> (`map` tiles) | [Main panel](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-stable-panel-main/) <br> [Balancers panel](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=service_total;) <br> [Rate limiter panel](https://yasm.yandex-team.ru/template/panel/maps_core_renderer_cache-ratelimiter2-panel) (look at `maps_front_tiles_api@maps_core_renderer_cache` signal) |
| maps-core-jams-rdr-cache <br> (`trf` tiles) | [Main panel](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-cache-stable-panel-main/) <br> [Balancers panel](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-rdr-cache.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-jams-rdr-cache-maps;signal=service_total) |
| maps-core-personalized-poi-renderer <br> (`personalized_poi` tiles) | [Main panel](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-stable-panel-main/) |

## Logs
| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` <br/> https://yd.yandex-team.ru/stage/maps-front-tiles-api_production/logs |
| Nginx,Juggler Client, Push client | /var/log/supervisor/ |
| YT (maps) | `hahn.[home/logfeller/logs/maps-front-production-log]` [yql example](https://yql.yandex-team.ru/Operations/X8YiglPzVIxOzMKxJisfZzbThXSfCNEWd6gTmbF9WXw=) |
| YT (Y.Deploy) | `` arnold.`logs/deploy-logs/` ``gs [yql example](https://yql.yandex-team.ru/Operations/X1X695dg8hJMS-gPVhkDmD3HBcjUZuB5LB1DI_IgA8g=) |

## Developing
Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| CI | https://teamcity.yandex-team.ru/viewType.html?buildTypeId=mapsapi_TilesApi_RergressionLoadTests |
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=tiles-api |

*Based on [http-api-stub](https://a.yandex-team.ru/arc_vcs/maps/front/tools/http-api-stub)*
