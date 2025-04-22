# Organization widget

[![](https://badger.yandex-team.ru/github/maps/org-badge-api/dev/state.svg)](https://github.yandex-team.ru/maps/org-badge-api/commits/dev)

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-org-badge-api/ |
| CI | [Sandbox](https://sandbox.yandex-team.ru/tasks?desc_re=maps%2Forg-badge-api&owner=MAPS_FRONT&limit=20) |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-org-badge-api |

## Instances

| Environment | URL |
|---|---|
| Testing | https://l7test.yandex.ru/maps-reviews-widget/ |
| Production | https://yandex.ru/maps-reviews-widget/ |

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-org-badge-api_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-org-badge-api-production-app/ |

## Dashboard

| Type | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/panel/org-badge-api-deploy |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Capacity & Stability | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-org-badge-api |

## Documentation

`https://tech.yandex.ru/maps/mapstools/`

## Vault

#### TVM tickets

See `tvm.secret` section at `src/configs/[production|testing].ts` for yav secret ids.

## Developing

Check out [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
