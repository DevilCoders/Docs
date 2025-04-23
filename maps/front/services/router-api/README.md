# `router-api`

Public routing API.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-router-api |
| Deploy | https://yd.yandex-team.ru/projects/maps-front-router-api |
| Awacs Production | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-router-api.slb.maps.yandex.net/show |
| Reactor | https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Frouter-api |
| YT | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/router-api |
| YT Pool | https://yt.yandex-team.ru/hahn/scheduling/overview?pool=maps-front-router-api&tree=physical |
| Robot | https://staff.yandex-team.ru/robot-maps-2333 |
| RPS limiter | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-router-api/editor |

## Instances

| Environment | URL |
|---|---|
| Testing | `https://router-api.tst.c.map.yandex.net/` |
| Production | `https://api.routing.yandex.net/` |

## Documentation

Public documentation of the /v2/route endpoint - https://yandex.ru/dev/maps/router/doc/

Public documentation of the /v2/distancematrix endpoint - https://yandex.ru/dev/maps/distance_matrix/doc/

Previous incarnations - [router-api](https://gitlab.yandex-team.ru/maps-legacy/router-api) [routing_public_api](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/routing_public_api?rev=r9406626)

## Known clients

The service is external, and access is granted via `apikey`. A full list of clients is kept by the Maps API sales team.

## What happens when service is down

Our clients do not receive the services that they paid for.

## How to fix common problems

### Restart service
```
# supervisorctl restart node
```

### Change log level
0. ssh to the desired instance.
1. Open the config file `vim /usr/local/app/out/config.js`.
2. Find the `logger` section.
3. Change the `level` property to one for the [supported ones](https://github.com/winstonjs/winston#logging-levels).
4. Restart the service.

**Note.** Do not forget to change the log level to the previous value, when you've finished debugging.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-router-api_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-router-api-production-app |


## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-router-api_production;mode=full |


## Upstream dashboards

| Name | URL |
|---|---|
| apikeys-int | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-apikeys-int_production |
| core-driving-router | https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-stable-panel-main |
| core-massstransit-router | https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-stable-panel-main |
| core-driving-matrix-router | https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-stable-panel-main/ |
| core-masstransit-matrix | https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-matrix;ctype=prestable,stable/ |

## Logs

| Name | path | URL | Example |
|---|---|---|---|
| NodeJS stderr | `/porto_log_files/app_workload_stderr.portolog` | | |
| NodeJS stdout | `/porto_log_files/app_workload_stdout.portolog` | [arnold.[logs/deploy-logs/1d]](https://yt.yandex-team.ru/arnold/#page=navigation&path=//logs/deploy-logs/1d) | [YQL](https://yql.yandex-team.ru/Operations/Yn5sba5OD4EIK4mTOam8pS58VPZCncrRhJN2pWtt_Hs=) |
| Nginx errors | `/var/log/nginx/error.log` | | |
| Nginx access | `/var/log/nginx/access-tskv.log` | [hahn.[home/logfeller/logs/maps-front-production-log/1d]](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/logfeller/logs/maps-front-production-log/1d) | [YQL](https://yql.yandex-team.ru/Operations/Yn5tfpfFtzmED6NsDEakmkfrnbU3Am_Fp7VGUyAYcR4=) |
| Nginx, Juggler Client, Push client | /var/log/supervisor/ | | |

## Regression Stress Testing Configurations

*TBA*

## Vault

Production - https://yav.yandex-team.ru/secret/sec-01fz0yyh8b6peve2rnkf5rr2nw/explore/versions
Testing - https://yav.yandex-team.ru/secret/sec-01fyy7by85qkxenc133x2c96qg/explore/versions

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://a.yandex-team.ru/arc_vcs/maps/front/tools/http-api-stub)*
