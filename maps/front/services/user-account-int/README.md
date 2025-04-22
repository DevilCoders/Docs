# user-account-int

[![oko health](https://badger.yandex-team.ru/oko/repo/maps/user-account-int/health.svg)](https://oko.yandex-team.ru/repo/maps/user-account-int)

User-account service provides information about user activity in Yandex.Maps applications.

## General Information

| Key | Value |
|---|---|
| ABC | <https://abc.yandex-team.ru/services/maps-front-user-account-int/> |
| Deploy | <https://deploy.yandex-team.ru/projects/maps-front-user-account-int> |

## Instances

| Environment | URL |
|---|---|
| Testing | <http://user-account-int.tst.c.maps.yandex.net/> |
| Production | <https://user-account-int.c.maps.yandex.net/> |

## Secrets

| Environment | URL |
|---|---|
| Testing | https://yav.yandex-team.ru/secret/sec-01ecykaccm5xx8sm5dgwysadfw/explore/version/ver-01ecykahqvdwn3kqbyj2y9js4g |
| Production | https://yav.yandex-team.ru/secret/sec-01ecykteq0cdx8fxmhcjam9dhp/explore/version/ver-01ecyktkqjzyv9rav1bq1d9dqv |

## Known clients

| Name | Origin |
|---|---|
| [Mobile maps proxy](https://github.yandex-team.ru/mapsapi/mobmaps-proxy) | mobmaps-proxy |

## API Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## What happens when service is down

Mobile maps cloudn't show user account data (user feedback, UGC activity).

## How to fix common problems

[How to detach instance from balancer](https://wiki.yandex-team.ru/maps/dev/ui/deploy/devops/#kakotkljuchitodininstansotbalansera)

### Restart instance

SSH into container, then:

```sh
supervisorctl restart app
```

## Blackbox grants

* Pass-test: https://grantushka.yandex-team.ru/grants/issue/21441/
* Mimino, prod: https://grantushka.yandex-team.ru/grants/issue/22339/

## Monitorings

| Type | URL |
|---|---|
| Juggler | <https://juggler.yandex-team.ru/?query=host%3Dmaps-front-user-account-int_production.app> |

## Dashboards

| Name | URL |
|---|---|
| Golovan | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-user-account-int_production/> |

## Backend dashboards

| Name | URL |
|---|---|
| UGC search | <https://yasm.yandex-team.ru/template/panel/ugcserver_requests/> |
| UGC search (org_api) | <https://yasm.yandex-team.ru/template/panel/ugcserver_requests/module%3Dapi%2Forg_api/> |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` <br/> <https://deploy.yandex-team.ru/stage/maps-front-user-account-int_production/logs>|
| Nginx, Juggler Client, Push client | /var/log/supervisor/ |
| YT (maps) | [example](https://yql.yandex-team.ru/Operations/XTHAtAlcTvze1pM64V-_tXyJPuPUl71jwRe3Th2sS50=) |

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
