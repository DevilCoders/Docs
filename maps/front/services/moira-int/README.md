# moira-int

[![oko health](https://badger.yandex-team.ru/oko/repo/maps/moira-int/health.svg)](https://oko.yandex-team.ru/repo/maps/moira-int)

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-moira-int/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-moira-int |

## Instances

| Environment | URL |
|---|---|
| Testing | https://moira-int.tst.c.maps.yandex.net/ |
| Production | https://moira-int.c.maps.yandex.net/ |

## Known clients
| Name | Origin |
|---|---|
| [Mobile maps proxy](https://a.yandex-team.ru/arc_vcs/maps/front/services/mobmaps-proxy-api) | mobmaps-proxy |

## API Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## What happens when service is down


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
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-moira-int_production.app |

## Dashboards

| Name | URL |
|---|---|
| Application (testing) | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-moira-int_testing |
| Applocation (production) | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-moira-int_production |
| DB | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbrngmohfiv83rf8aub;dbname=maps_moira_int_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` <br/> https://deploy.yandex-team.ru/stages/maps-front-moira-int_production/logs |
| Nginx errors | `/var/log/nginx/error.log` |
| Nginx access | `/var/log/nginx/access.log` |
| YT (maps) | [yql example](https://yql.yandex-team.ru/Operations/XS2DpmHljqJ3lhtcrep5d3fi65DnUMlzDRwAhnvZHHI=) |
| YT (qloud) | [yql example](https://yql.yandex-team.ru/Operations/XS2Du2HljqJ3lhtm7NjFXgk57Ol66kZFnjNpYkMrDDg=) |

*Based on [http-api-stub](https://a.yandex-team.ru/arc_vcs/maps/front/tools/http-api-stub)*
