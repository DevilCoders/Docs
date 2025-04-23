# `{{Add project name}}` `{{Add CI ICON}}`
`{{Add project description}}`

## General information

| Key | Value |
|---|---|
| Product manager | https://staff.yandex-team.ru/{{PRODUCTMANAGER}} |
| Project manager | https://staff.yandex-team.ru/{{PROJECTMANAGER}} |
| Designer | https://staff.yandex-team.ru/{{DESIGNER}} |
| Maintainers | https://staff.yandex-team.ru/{{MAINTEINER1}} <br/> https://staff.yandex-team.ru/{{MAINTEINER2}} <br/> https://staff.yandex-team.ru/{{MAINTEINER3}} |
| SRE | https://staff.yandex-team.ru/morbid <br/> https://staff.yandex-team.ru/kartvep |
| Tracker Queue | `{{Add url to queue in Startrek}}` |
| Repository | `{{Add url to repository in Github}}` |
| CI | `{{Add url to project in TeamCity}}` |
| RTC | `{{Add url to project in Nanny}}` |
| Statistics | `{{Add url to project in Statface}}` |
| Tanker | `{{Add url to project in Tanker}}` |
| `SOMESERVICE` | `{{Add url to project in any other service}}` |

## Instances

| Environment | URL |
|---|---|
| Testing | `{{Add url to service in testing}}` |
| Prestable | `{{Add url to service in prestable}}` |
| Production | `{{Add url to service in production}}` |

## Documentation

`{{Add links to documentation about service}}`

## Known clients

`{{Add links to clients of the service}}`

## Blackbox grants

`{{Blackbox grant can be found in https://grantushka.yandex-team.ru/grants/consumer/}}`

For example,

> | allow_login| strict |
> | allow_oauth |
> | allow_user_info |

## What happens when service is down

`{{Describe what happens when service part or the whole service is unavailable. Is it possible to degradate? Describe it, too, if so}}`

For example,

> Mobile Yandex Maps stops handling SEO urls. It means that if a user clicks on a such url, he or she will see only home region without search request, route, and etc.

## How to fix common problems

`{{Describe what SRE should do to resuscitate service: how to restart service, change log levels, and fix some known issues}}`

See [mobmaps-proxy-api](https://github.yandex-team.ru/mapsapi/mobmaps-proxy#how-to-fix-common-problems) example.

## SLA

`{{Add link to SLA configuration from https://a.yandex-team.ru/arc/trunk/arcadia/maps/monitoring/tools/sla_calculator/core/services)}}`

## Monitorings

| Type | URL |
|---|---|
| Juggler | `{{Add url to service in juggler}}` |

For example,

> | Type | URL |
> |---|---|
> | Juggler | https://juggler.yandex-team.ru/?query=host%3Dqloud-ext.maps.apple-search-api.nodejs |

## Dashboards

| Name | URL |
|---|---|
| Golovan | `{{Add path in golovan pannel}}` |

For example,

> | Name | URL |
> |---|---|
> | Goloval | https://yasm.yandex-team.ru/panel/maps_core_meta_stable |

## Logs

| Name | URL/path |
|---|---|
| Nginx, DoBlu Agent, Juggler Client, Push client | `{{Add path to logs file}}` |
| YT  | `{{Add path to logs file}}` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | `Add url to your projects regression graphics` |
| CI | `Add url to your stress testing regression in CI` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
