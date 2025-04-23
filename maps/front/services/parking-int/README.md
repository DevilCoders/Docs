# `parking-int`

Internal HTTP API that provides methods for paying for public parking sessions

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-parking-int |
| Deploy | https://yd.yandex-team.ru/projects/maps-front-parking-int |

## Instances

| Environment | URL |
|---|---|
| Testing | `parking-int.tst.c.maps.yandex.net` |
| Prestable | `{{Add url to service in prestable}}` |
| Production | `{{Add url to service in production}}` |

## MDB Clusters
| Environment | ClusterID | Link |
|---|---|---|
| `testing` | `mdb911l8qmj0j77k7or2` | https://yc.yandex-team.ru/folders/akuu416mk63jvfb4ep52/managed-postgresql/cluster/mdb911l8qmj0j77k7or2 |
| `production` | `mdberta23qpqt3jlhf6o` | https://yc.yandex-team.ru/folders/akuu416mk63jvfb4ep52/managed-postgresql/cluster/mdberta23qpqt3jlhf6o |

## Documentation

`{{Add links to documentation about service}}`

## Known clients

- via `geointernal.mob.maps.yandex.net` https://github.yandex-team.ru/maps/mobmaps-proxy-api
  - Mobile Maps https://abc.yandex-team.ru/services/mobilemaps/
  - Mobile Navigator https://abc.yandex-team.ru/services/mobilenavi/

## What happens when service is down

`{{Describe what happens when service part or the whole service is unavailable. Is it possible to degradate? Describe it, too, if so}}`

For example,

> Mobile Yandex Maps stops handling SEO urls. It means that if a user clicks on a such url, he or she will see only home region without search request, route, and etc.

## How to fix common problems

`{{Describe what SRE should do to resuscitate service: how to restart service, change log levels, and fix some known issues}}`

See [mobmaps-proxy-api](https://github.yandex-team.ru/mapsapi/mobmaps-proxy#how-to-fix-common-problems) example.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-parking-int_production.app |
| Golovan |	https://yasm.yandex-team.ru/template/alert/maps-front-parking-int-production-app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-parking-int_production |

## Upstream/dependency dashboards

Dashboards of the services using (`upstream`) or used by (`dependency`) this service.

| Name | URL |
|---|---|
| Backend1 | `{{Add url to service in yasm / graphana}}` |

For example,

> | Name | URL |
> |---|---|
> | Keyserv (Graphania) | https://grafana.yandex-team.ru/d/5ix94-Smk/maps-keyserv-back?orgId=1 |
> | Apikeys (Graphania) | https://grafana.yandex-team.ru/d/6mcvzSNmk/maps-apikeys-back?orgId=1 |
> | Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-parking-int_production |

## Logs

| Name | URL/path |
|---|---|
| Deploy | `{{Add url to logs in the Deploy UI}}` |
| Nginx, DoBlu Agent, Juggler Client, Push client | `{{Add path to logs file}}` |
| YT  | `{{Add path to logs file}}` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | `Add url to your projects regression graphics` |
| CI | `Add url to your stress testing regression in CI` |

## Vault

| Type | URL |
|---|---|
| Testing | https://yav.yandex-team.ru/secret/sec-01f8z1ebp750pma0c5j1kp2b31 |
| Production | https://yav.yandex-team.ru/secret/sec-01fcxf15kdbsyycjx1fnrtmh4r |


## Transfer Manager

| Type | URL |
|---|---|
| Testing Transfer | https://yc.yandex-team.ru/folders/akuu416mk63jvfb4ep52/data-transfer/transfer/dtt3scr66ank1ctjtlj8/view |
| Testing YT Data | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/parking-int/db-replication/testing |
| Production Transfer | https://yc.yandex-team.ru/folders/akuu416mk63jvfb4ep52/data-transfer/transfer/dttpvpcej720qleo01ba/view |
| Production YT Data | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/parking-int/db-replication/production |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
