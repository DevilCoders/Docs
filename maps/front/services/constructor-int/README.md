# constructor-int

Provides REST API for mymaps and constructor databases.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-constructor-int |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-constructor-int |
| CI | [Sandbox](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&order=-updated&owner=MAPS_FRONT&forPage=tasks&desc_re=maps%2Fconstructor-int) |
| Key in [inthosts](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts) | `constructorInt` |

## Instances

| Environment | URL |
|---|---|
| Testing | http://constructor-int.tst.c.maps.yandex.net |
| Production | http://constructor-int.maps.yandex.net |
| GDPR testing | https://constructor-int.gdpr.tst.slb.maps.yandex.net |
| GDPR production | https://constructor-int.gdpr.maps.yandex.net |

## Storage

* MDB clusters: https://yc.yandex-team.ru/folders/foocivevdte4nc28jstn/managed-postgresql

## Documentation

API method documentation in [swagger](http://swagger.io/specification/) format can be found in
[docs](docs) directory.

## Known clients

* [constructor][constructor]: shows and allows to edit user maps.
* [constructor-api][constructor-api]: shows public maps on external sites.
* [maps][maps]: shows public or private maps by link.
* [takeout][takeout]: requests data for GDPR.

[constructor]: https://a.yandex-team.ru/arc_vcs/maps/front/services/constructor
[constructor-api]: https://a.yandex-team.ru/arc_vcs/maps/front/services/constructor-api
[maps]: https://a.yandex-team.ru/arc_vcs/maps/front/services/maps
[takeout]: https://wiki.yandex-team.ru/passport/takeout/

## What happens when service is down

* [constructor][constructor]: will stop to show and edit user maps.
* [constructor-api][constructor-api]: will stop to show user maps.
* [maps][maps]: will stop to show user maps.
* [takeout][takeout]: will stop to load data for GDPR.

## Troubleshooting

### Disable public maps for user
Service allows to disable public maps for a specific `uid` via `config['app.shadowban.uids']`:

1. Fast (qeq distribute + restart app):
```sh
# Repeat per DC (`vla`, `man`, `sas`)
# Distribute a file with config overrides that bans specific uids
echo '{"app.shadowban.uids": ["uid1", "uid2"]}' > app-config-overrides.json
qeq distribute yd:maps-front-constructor-int_production.app.app_box@DC app-config-overrides.json /etc/yandex/maps

# Gracefully restart the app
qeq exec yd:maps-front-constructor-int_production.app.app_box@DC -- %"instancectl close && sleep 15 && supervisorctl restart app && sleep 5 && instancectl open"
```
2. Slow (redeploy): update env `MAPS_APP_CONFIG_OVERRIDE` to contain `{"app.shadowban.uids": ["uid1", "uid2"]}`.
3. Permanent (docker + redeploy): add uid to `src/config.ts`.

## Monitorings

| Type | URL |
|---|---|
| Juggler (main) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-constructor-int_production.app |

## Dashboards

| Name | URL |
|---|---|
| Production | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-constructor-int_production |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-constructor-int_testing |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| Cron | `/run/qloud/app.syslog` |
| YT | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-constructor-int_app"` |
| stdout/stderr | ``arnold.`logs/deploy-logs/1d/` ``, `stage = 'maps-front-constructor-int_production'` |

## Regression Stress Testing Configuration

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-constructor-int |
| CI | https://sandbox.yandex-team.ru/scheduler/17559/view |

## Grants

* [takeout](https://grantushka.yandex-team.ru/grants/issue/16717/): for test integration with `Takeout`.

## Vault

* [constructor-int-testing](https://yav.yandex-team.ru/secret/sec-01cn1qn22sgzkn6d5mwfjrer0m)
* [constructor-int-production](https://yav.yandex-team.ru/secret/sec-01cn1zra9fm7ymm37z55fp2an8)
* [robot-maps-ctor](https://yav.yandex-team.ru/secret/sec-01d6gd1z5r9mqw09218d3akdxj): for access to
  YT during processing deleted accounts.

## Troubleshooting

* `takeout`: look into `maintainance` stdout/stderr, `deleted_maps_log` table
* `takeout/delete`: look into stdout/stderr (grep by `request_id`), `deleted_maps_log` table
* `sync-deleted-uids` scheduler: [see here](schedulers/sync-deleted-uids/README.md#troubleshooting).

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
