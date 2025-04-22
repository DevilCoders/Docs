# Geomedia advert landing page
Static promo page.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-promo-brand-platform/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-promo-brand-platform |

## Instances

| Environment | URL |
|---|---|
| Testing | https://l7test.yandex.ru/maps-promo/brand/ |
| Production | https://yandex.ru/maps-promo/brand/ |

| Balancer | AWACS |
|---|---|
| Testing | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-promo-brand-platform/show |
| Production | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps-promo.slb.maps.yandex.net/upstreams/list/maps-front-promo-brand-platform/show |

## Storage

 * MDS S3 bucket: https://yastatic.net/s3/front-maps-static/front-promo-brand-platform/


## Known clients

External people. Ask about partners: [@npolskaya](https://staff.yandex-team.ru/npolskaya).

## What happens when service is down

People will not be able to open a webpage.

## How to fix common problems

### Start, stop or restart instance
SSH into container, then:

`supervisorctl [restart|start|stop] node`

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host=maps-front-promo-brand-platform_production.app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-promo-brand-platform_production;mode=full |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | [Deploy](https://deploy.yandex-team.ru/stages/maps-front-promo-brand-platform_production/logs) <br/>`logs`, `logs stderr` |
| Nginx | `/var/log/nginx/` |
| Logs for all processes in container | `/var/log/supervisor/` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
