# `Factory v2`
`The service allows content managers to edit and publish raw satelite images`

## General information

| Key | Value |
|---|---|
| ABC | [https://abc.yandex-team.ru/services/maps-front-factory-admin/](https://abc.yandex-team.ru/services/maps-front-factory-admin/) |
| Deploy | [https://deploy.yandex-team.ru/projects/maps-front-factory-admin](https://deploy.yandex-team.ru/projects/maps-front-factory-admin) |
| Tanker | [https://tanker.yandex-team.ru/?project=ymaps-factoryadmin](https://tanker.yandex-team.ru/?project=ymaps-factoryadmin) |

## Instances

| Environment | URL |
|---|---|
| Testing | [https://factory-admin.tst.c.maps.yandex-team.ru/](https://factory-admin.tst.c.maps.yandex-team.ru/) |
| Production | [https://factory-admin.maps.yandex-team.ru/](https://factory-admin.maps.yandex-team.ru/) |

## Known clients

`Service is used by content managers`

## What happens when service is down

`Content managers cannot edit and publish satelite images`

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-factory-admin_production.app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-factory-admin_production |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stages/maps-front-factory-admin_production/logs |
| Nginx | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log/1d `tskv_format='maps-front-factory-admin_app'` |
| YT  | https://yt.yandex-team.ru/arnold/navigation?path=//logs/deploy-logs/1d `project='maps-front-factory-admin'` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
