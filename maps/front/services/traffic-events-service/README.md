# Traffic Events Service [![build status](https://badger.yandex-team.ru/github/maps/traffic-events-service/master/state.svg)](https://github.yandex-team.ru/maps/traffic-events-service/commits/master)

JS-hand for road events

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-traffic-events-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-traffic-events-service |

## Instances

| Environment | URL | Stage |
|---|---|---|
| Testing | [traffic-events-service.tst.c.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-traffic-events-service/show/) | https://deploy.yandex-team.ru/stage/maps-front-traffic-events-service_testing/ |
| Production | [traffic-events-service.c.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-traffic-events-service.slb.maps.yandex.net/show/) | https://deploy.yandex-team.ru/stage/maps-front-traffic-events-service_production |

## Dashboards
| Name | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-traffic-events-service_production |
| Balancer porto | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-traffic-events-service.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-traffic-events-service.slb.maps.yandex.net/ |
| Balancer requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-traffic-events-service.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-traffic-events-service.slb.maps.yandex.net/ |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-traffic-events-service_production.app |
| YASM Checks | https://yasm.yandex-team.ru/template/alert/maps-front-traffic-events-service-production-app |

## Backend dashboards

| Name | URL |
|---|---|
| infopoints | https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-stable-panel-main |
| core-jams-info | https://yasm.yandex-team.ru/template/panel/maps-core-jams-info-stable-panel-main |
| core-jams-rdr | https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-stable-panel-main |

## Documentation

## Known clients

[jsapi-v1.1]: https://github.yandex-team.ru/maps/jsapi-v1.1
[jsapi-v2.0]: https://github.yandex-team.ru/maps/jsapi-v2.0
[jsapi-v2.1]: https://github.yandex-team.ru/maps/jsapi-v2.1

- [jsapi-v1.1][jsapi-v1.1]
- [jsapi-v2.0][jsapi-v2.0]
- [jsapi-v2.1][jsapi-v2.1]

## What happens when service is down

Traffic, road accidents and traffic light in [jsapi-v1.1 [jsapi-v1.1], [jsapi-v2.0][jsapi-v2.0] and [jsapi-v2.1][jsapi-v2.1] will stop working.

## How to fix common problems
### Restart service
```
supervisorctl restart node
```

## Logs

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stage/maps-front-traffic-events-service_production/logs |
| Supervisor | `/var/log/supervisor/` |
| YT  | hahn.`home/logfeller/logs/maps-front-production-log` [yql example](https://yql.yandex-team.ru/Operations/X5qx8mim9cB5qR5SBlIzXmUx37ftOSqqLpmKZ-DoFPA=) |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
