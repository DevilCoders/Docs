# regions-service

Hosts static files with regions description from mds.

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-regions-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-regions-service |
| Balancer | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-jsapi.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-jsapi.slb.maps.yandex.net;signal=service_total |

## Instances

| Environment | URL |
|---|---|
| Testing | https://api-maps.tst.c.maps.yandex.ru/services/regions/ |
| Production | https://api-maps.yandex.ru/services/regions/ |

## Storage

 * MDS S3 bucket: `regions-service`

## Known clients

[Yandex maps API](https://github.yandex-team.ru/mapsapi/jsapi-v2)

## API Documentation

API method documentation and API enitities description can be found in [docs](docs) directory.

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-regions-service_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-regions-service-production-app |

## Dashboards

| Name | URL |
|---|---|
| Golovan | [https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-regions-service_production](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-regions-service_production) |
## Logs
| Name | URL/path |
|---|---|
| Nginx, Juggler Client, Push client | /var/log/supervisor/ |
| YT (maps) | `hahn.[logs/mhome/logfeller/logs/maps-front-production-log]` [yql example](https://yql.yandex-team.ru/Operations/X5qzCBpqv1DWZfWmKdDkG657roIpoQ6xNfaLNnrRHTc=) |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Capacity | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-regions-service |
| Stability | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-regions-service%20const |

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
