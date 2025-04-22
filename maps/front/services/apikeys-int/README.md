# apikeys-int

Provides API key validation logic for Yandex Maps JS API and services.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-apikeys-int/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-apikeys-int |
| CI | [Sandbox](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&order=-updated&owner=MAPS_FRONT&forPage=tasks&desc_re=maps%2Fapikeys-int) |
| Key in [inthosts](https://github.yandex-team.ru/maps/hosts) | `apikeysInt` |

## Instances

| Environment | URL |
|---|---|
| Testing | http://apikeys-int.tst.c.maps.yandex.net/ |
| Production | http://apikeys-int.c.maps.yandex.net/ |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Known clients

* [search-service]
* [geocode-search-api]
* [router-service]
* [geoxml-service]
* [constructor-api]
* [panoramas-service]
* [tiles-api]

[search-service]: https://github.yandex-team.ru/maps/search-service
[geocode-search-api]: https://github.yandex-team.ru/maps/geocode-search-api
[router-service]: https://github.yandex-team.ru/maps/router-service
[geoxml-service]: https://github.yandex-team.ru/maps/geoxml-service
[constructor-api]: https://github.yandex-team.ru/maps/constructor-api
[panoramas-service]: https://github.yandex-team.ru/maps/panoramas-service
[tiles-api]: https://github.yandex-team.ru/maps/tiles-api

## What happens when service is down

The following services will stop to check restrictions:

* [search-service]
* [geocode-search-api]
* [router-service]
* [geoxml-service]
* [constructor-api]
* [panoramas-service]
* [tiles-api]

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-apikeys-int_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-apikeys-int_production |
| Keys synchronization | https://yasm.yandex-team.ru/chart/signals=unistat-keys_*;hosts=ASEARCH;itype=deploy;deploy_unit=app;stage=maps-front-apikeys-int_production/?term=maps-front-apikeys-int_production |
| Batcher keys synchronization | https://yasm.yandex-team.ru/chart/signals=unistat-batcher_*;hosts=ASEARCH;itype=deploy;deploy_unit=app;stage=maps-front-apikeys-int_production/?term=maps-front-apikeys-int_production |


Keys synchronization signals:

* `keys_<service>_sync_lag_axxx`: Synchronization lag in seconds.
* `keys_<service>_sync_duration_axxx` Last successful synchronization duration is seconds.
* `keys_<service>_sync_errors_annn` Number of failed synchronizations.
* `keys_<service>_update_lag_axxx`: Keys update lag in seconds. This value is reset when keys are
  changed during synchronization.

Where `<service>` is a service name in `apikeys` backend.

## Backend dashboards

| Name | URL |
|---|---|
| apikeys | https://grafana.yandex-team.ru/d/6mcvzSNmk/maps-apikeys-back?orgId=1 |
| keyserv | https://yasm.yandex-team.ru/template/panel/maps-core-keyserv-stable-panel-main |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stages/maps-front-apikeys-int_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` `` |

## Troubleshooting

### `apikey` was not valid long after adding it on developer.tech.yandex.ru
1. Check that key is present in https://admin-developer.tech.yandex-team.ru/ (if you have the rights)
2. Check key dumps on instances to see in what state the key was in `/var/cache/apikeys-int/apimaps/dumps/`
    ```
    # cd /var/cache/apikeys-int/apimaps/dump/
    # grep -nri foo-bar-baz .
    /var/cache/apikeys-int/apimaps/dump/2021-01-23T04:19:43.066Z:121947:{"id":"foo-bar-baz","tariff":"apimaps_free","hostnameRe":null,"ipAddresses":null,"ipNetworks":null,"hostnames":null}
    ...
    # grep -nri foo-bar-baz 2021-01-25T10* # limit by time (NB: time is in UTC)
    # cd /var/cache/apikeys-int/city/dump/ # search-api is in different apikeys project, hence different directory
    ```

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-apikeys-int |
| CI | https://sandbox.yandex-team.ru/scheduler/13401/view |

## Vault

* [maps-front-apikeys-int.production](https://yav.yandex-team.ru/secret/sec-01eyrrzaa8dc3j6tpp8ebrnw33)
* [maps-front-apikeys-int.testing](https://yav.yandex-team.ru/secret/sec-01eyjh8mwqh7k2pw1h26rp7gkm)
* [maps-front-apikeys-int.stress](https://yav.yandex-team.ru/secret/sec-01eyzdg1c9vwxx5rz8etcbcx8j)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://github.yandex-team.ru/mapsapi/http-api-stub)*
