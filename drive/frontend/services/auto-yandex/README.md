# maps-front-promo-auto-yandex

[![oko health](https://badger.yandex-team.ru/oko/repo/maps/promo-auto-yandex/health.svg)](https://oko.yandex-team.ru/repo/maps/promo-auto-yandex)

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-promo-auto-yandex/ |
| CI | https://sandbox.yandex-team.ru/tasks?desc_re=maps%2Fspecprojects&owner=MAPS_FRONT |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-promo-auto-yandex |

## Instances
| Environment | URL |
|---|---|
| Testing | https://promo-auto.tst.c.maps.yandex.ru/ |
| Production | https://auto.yandex/ |

### Internal handlers

| Environment | URL |
|---|---|
| Testing | https://promo-auto-int.tst.c.maps.yandex.net/ |
| Production | https://promo-auto-int.c.maps.yandex.net/ |

Internal client: https://forms.yandex-team.ru/ext/admin/10010537/

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## How to fix common problems

[How to detach instance from balancer](https://wiki.yandex-team.ru/maps/dev/ui/deploy/devops/#kakotkljuchitodininstansotbalansera)

### Restart instance

SSH into container, then:

```sh
supervisorctl restart node
```

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-promo-auto-yandex-production.app |

## Dashboards

| Name | URL |
|---|---|
| Application | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-promo-auto-yandex_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stages/maps-front-promo-auto-yandex_production/logs |
| Nginx, Juggler Client, Push client | /var/log/supervisor/ |

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
