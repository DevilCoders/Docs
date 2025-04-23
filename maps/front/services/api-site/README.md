# `api-site`
`Site for Maps Api`

## General information

| Key | Value                                                           |
|---|-----------------------------------------------------------------|
| ABC | https://abc.yandex-team.ru/services/maps-front-api-site         |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-api-site |
| Tanker | https://tanker.yandex-team.ru/project/maps-front-api-site |

## Instances

| Environment | URL |
|---|---|
| Testing | https://api-site.tst.c.maps.yandex.ru/ |
| Prestable | `{{Add url to service in prestable}}` |
| Production | `{{Add url to service in production}}` |

## Storage

 * MDS S3 bucket: `{{Add name of the bucket used by this application}}`
 * MDS Avatars namespace: `{{Add the namespace used by this application}}`
 * MDS namespace: `{{Add the namespace used by this application}}`
 * MDB cluster name: `{{Add the name of the cluster used by this application}}`
 * `{{Please fill in name and identifier for other storage service}}`

## Monitorings

| Type | URL |
|---|---|
| Juggler | `{{Add url to service in juggler}}` |

## Dashboards

| Name | URL |
|---|---|
| YASM | `{{Add url to service in yasm}}` |

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
