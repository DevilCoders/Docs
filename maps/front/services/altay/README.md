# Altay

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-altay/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-altay |
| Tanker | https://tanker.yandex-team.ru/project/maps-front-altay |

## Instances

| Environment | URL |
|---|---|
| Testing | https://altay.tst.c.maps.yandex-team.ru/ |
| Production | `{{Add url to service in production}}` |

## Documentation

https://docs.yandex-team.ru/sprav/

## Known clients

Service is used by content managers.

## What happens when service is down

Users aren't able to edit business info.

## How to fix common problems

### Restart service
```
# supervisorctl restart node
```

### Change log level
0. ssh to the desired instance.
1. Open the config file `vim /usr/local/app/configs/production.yaml`.
2. Find the `logger` section.
3. Change the `level` property to one for the [supported ones](https://github.com/winstonjs/winston#logging-levels).
4. Restart the service.

**Note.** Do not forget to change the log level to the previous value, when you've finished debugging.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-altay_production.app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-altay_production |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-altay_production/logs |
| Nginx | [hahn.[home/logfeller/logs/maps-front-production-log/1d]](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/logfeller/logs/maps-front-production-log/1d) tskv_format='maps-front-altay_app"' |
| NodeJS  | [arnold.[logs/deploy-logs/1d]](https://yt.yandex-team.ru/arnold/#page=navigation&path=//logs/deploy-logs/1d) stage='maps-front-altay_production' |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
