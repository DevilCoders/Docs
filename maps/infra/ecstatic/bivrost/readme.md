# Bifröst

Realtime datasets replication service

Uploads datasets from postdl hoot to other ecstatic environment

## General information

| Key | Value |
|---|---|
| Maintainers | https://staff.yandex-team.ru/nikitonsky <br/>  |
| Tracker Queue | https://st.yandex-team.ru/GEOINFRA |

## Service infrastructure

| Environment | Nanny | Juggler | Yasm |
|---|---|---|---|
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_bivrost_testing/ | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_bivrost_testing | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-bivrost-testing-panel-main/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_bivrost_stable/ | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_bivrost_stable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-bivrost-stable-panel-main/ |


## Ecstatic environments

| Environment | download | upload |
|---|---|---|
| Testing | stable | unstable |
| Stable | stable | datatesting |

## Known clients

- maps_core_driving_driver_datatesting
- maps_core_driving_router_datatesting
- maps_core_masstransit_router_datatesting

## Logs

| Name | Path |
|---|---|
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/ |

## What happens when service is down

Data replication stops
