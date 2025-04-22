# Constructor API

[![production version](https://badger.yandex-team.ru/qloud/maps/front-constructor-api/production/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-constructor-api/production) [![testing version](https://badger.yandex-team.ru/qloud/maps/front-constructor-api/testing/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-constructor-api/testing)

Yandex Map Constructor Widget. Allows to insert a map from Yandex Map Constructor into a site.

## General information
| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-constructor-api/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-constructor-api/ |
| Tanker | https://tanker.yandex-team.ru/?project=constructor3&branch=master&keyset=constructor-service |

## Instances
| Environment | URL |
|---|---|
| Testing | https://api01e.tst.maps.yandex.ru/services/constructor/ |
| Production | https://api-maps.yandex.ru/services/constructor/ |

## Documentation
* [API](https://tech.yandex.ru/maps/doc/constructor/concepts/About-docpage/?from=mapstools)

## What happens when service is down
Constructor's maps will stop displaying on external sites.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-constructor-api_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-constructor-api-production-app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-constructor-api_production |

## Backend dashboards

| Name | URL |
|---|---|
| constructor-int | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-constructor-int_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` <br/> https://deploy.yandex-team.ru/stage/maps-front-constructor-api_production/logs |
| Supervisor | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-constructor-api_app"`) |

## Developing
Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
