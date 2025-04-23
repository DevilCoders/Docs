# `{{Add project name}}`
`{{Add project description}}`

[![oko health](https://badger.yandex-team.ru/oko/repo/maps/{{project-name}}/health.svg)](https://oko.yandex-team.ru/repo/maps/{{repo-name}})

## General information

| Key | Value |
|---|---|
| ABC | `{{Add url to project in ABC}}` (see [rules](https://wiki.yandex-team.ru/maps/dev/ui/deploy/#abc)) |
| Deploy | `{{Add url to project in Deploy}}` |
| Statistics | `{{Add url to project in Statface}}` |
| Tanker | `{{Add url to project in Tanker}}` |
| Grantushka ID | `{{Add the ID of your service in Grantushka}}` |
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

See [mobmaps-proxy-api](https://a.yandex-team.ru/arcadia/maps/front/services/mobmaps-proxy-api#how-to-fix-common-problems) example.

## Monitorings

| Type | URL |
|---|---|
| Juggler | `{{Add url to service in juggler}}` |

For example,

> | Type | URL |
> |---|---|
> | Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-{{ProjectName}}_production.app |

## Dashboards

| Name | URL |
|---|---|
| YASM | `{{Add url to service in yasm}}` |

For example,

> | Name | URL |
> |---|---|
> | Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-{{ProjectName}}_production |

## Backend dashboards

| Name | URL |
|---|---|
| Backend1 | `{{Add url to service in yasm}}` |

For example,

> | Name | URL |
> |---|---|
> | Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-{{ProjectName}}_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `{{Add path to logs file}}` |
| Nginx, DoBlu Agent, Juggler Client, Push client | `{{Add path to logs file}}` |
| YT  | `{{Add path to logs file}}` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | `Add url to your projects regression graphics` |
| CI | `Add url to your stress testing regression in CI` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
