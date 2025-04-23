# `geodisplay-int`

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## General information

| Key | Value |
|---|---|
| ABC | `{{Add url to project in ABC}}` (see [rules](https://wiki.yandex-team.ru/maps/dev/ui/deploy/#abc)) |
| CI | `{{Add url to project in your CI system (e.g. TeamCity)}}` |
| Deploy | `{{Add url to project in Deploy}}` |
| `SOMESERVICE` | `{{Add url to project in any other service}}` |

## Instances

| Environment | URL |
|---|---|
| Testing | `{{Add url to service in testing}}` |
| Prestable | `{{Add url to service in prestable}}` |
| Production | `{{Add url to service in production}}` |

## Storage

 * MDS S3 bucket: `{{Add name of the bucket used by this application}}`
 * MDS Avatars namespace: `{{Add the namespace used by this application}}`
 * MDS namespace: `{{Add the namespace used by this application}}`
 * MDB cluster name: `{{Add the name of the cluster used by this application}}`
 * `{{Please fill in name and identifier for other storage service}}`

For example,

> * MDS S3 bucket: `metrokit-bundles`
> * MDB cluster name: `metrostroy`

## Documentation

`{{Add links to documentation about service}}`

## Known clients

`{{Add links to clients of the service}}`

## What happens when service is down

`{{Describe what happens when service part or the whole service is unavailable. Is it possible to degradate? Describe it, too, if so}}`

For example,

> Mobile Yandex Maps stops handling SEO urls. It means that if a user clicks on a such url, he or she will see only home region without search request, route, and etc.

## How to fix common problems

`{{Describe what SRE should do to resuscitate service: how to restart service, change log levels, and fix some known issues}}`

See [mobmaps-proxy-api](https://a.yandex-team.ru/arc_vcs/maps/front/services/mobmaps-proxy-api#how-to-fix-common-problems) example.

## Monitorings

| Type | URL |
|---|---|
| [Juggler](https://juggler.yandex-team.ru/) | `{{Add url to service in juggler}}` |
| [Golovan](https://yasm.yandex-team.ru/) | `{{Add url to service in YASM (aka Golovan)}}` |

For example,

> | Type | URL |
> |---|---|
> | Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-coverage-service_production.app |
> | Golovan |	https://yasm.yandex-team.ru/template/alert/maps-front-coverage-service-production-app |

## Dashboards

| Name | URL |
|---|---|
| Graphania | `{{Add url to service in graphana (if exists)}}` |
| YASM | `{{Add url to service in yasm}}` |

For example,

> | Name | URL |
> |---|---|
> | Main (Graphania) | https://grafana.yandex-team.ru/dashboard/db/maps-mobile-mapkit?orgId=1 |
> | UserAgents (Graphania) | https://grafana.yandex-team.ru/dashboard/db/maps-mobile-mapkit-clients?orgId=1 |
> | YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-geodisplay-int_production |

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
> | Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-geodisplay-int_production |

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

`{{Add links to secrets in https://yav.yandex-team.ru}}`

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://a.yandex-team.ru/arc_vcs/maps/front/tools/http-api-stub)*
