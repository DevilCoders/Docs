# `startup-service`

Provides initial data for JS API.

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-startup-service/ |
| Deploy| https://deploy.yandex-team.ru/projects/maps-front-startup-service |

## Instances

| Environment | URL |
|---|---|
| testing | https://api-maps.tst.c.maps.yandex.ru/services/startup/v1?lang=ru_RU |
| production | https://api-maps.yandex.ru/services/startup/v1?lang=ru_RU |

## Known clients

* ymaps3-react: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/ymaps3-react (all clients from `frontend monorepo` https://a.yandex-team.ru/search?search=ymaps3-react%22%3A%20%22,,Cj,arcadia,,200&repo=arc)

## What happens when service is down

`ymaps3-react` will not work and maps for all clients would not be loaded.

## How to fix common problems

Restart service:
```
# supervisorctl restart node
```

## Monitorings

| Type | URL |
|---|---|
| yasm | https://yasm.yandex-team.ru/template/alert/maps-front-startup-service-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-startup-service_production.app |

## Dashboards

| Name | URL |
|---|---|
| yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-startup-service_production |

## Upstream/dependency dashboards

| Name | URL |
|---|---|
| mapmeta | https://yasm.yandex-team.ru/template/panel/maps-core-meta-stable-panel-main/ |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stages/maps-front-startup-service_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-startup-service_app"` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Lunapark | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=maps-front-startup-service |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
