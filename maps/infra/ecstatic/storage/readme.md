[TOC]
# Maps-Core-Ecstatic-Storage

Provides a storage area for Ecstatic data

## Graphs
| Staging | URL |
|---|---|
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-storage-stable-panel-main/ |
| Prestable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-storage-prestable-panel-main/ |
| Datatesting | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-storage-datatesting-panel-main/ |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-storage-testing-panel-main/ |
| Unstable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-storage-unstable-panel-main/ |

## General information

| Topic | Information |
|---|---|
| Help | Алексей Хроленко (khrolenko@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ecstatic/ymtorrent |
| ABC service | https://abc.yandex-team.ru/services/maps-core-ecstatic-storage |
| CI (TestEnv) | https://beta-testenv.yandex-team.ru/project/maps_geoinfra_tests/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_ECSTATIC_STORAGE/history |

## Instances

| Environment | URL |
|---|---|
| Nanny services | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_storage_testing|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_storage_prestable|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_storage_stable|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_storage_datatesting|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_storage_unstable|
| Dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_ecstatic_storage|

## Known clients

[ecstatic tool](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#commandlinetoolreference)

## Documentation

https://wiki.yandex-team.ru/maps/dev/core/ecstatic/

## What happens when the service is down

This is a critical service. When it is down, generators can't upload any data. All the services that depend
on data delivery by Ecstatic stop getting fresh data. Important services such as Яндекс.Пробки become unreliable.

## How to fix common issues

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Also there have been some occurrences of a mass storage issue with RTC. Namely when there's no
space left on the device on which the directory `/var/lib/yandex/maps/ecstatic/torrents/` is mounted,
the command `df -h /var/lib/yandex/maps/ecstatic/torrents/` may erroneously indicate that there is
free space on this device. If it ever happens, contact the RTC support team and send a report such as
[this one](https://st.yandex-team.ru/RTCSUPPORT-2839).    

## Monitoring

| Staging | URL |
|---|---|
| Stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_storage_stable |
| Prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_storage_prestable |
| Datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_storage_datatesting |
| Testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_storage_testing |
| Unstable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_storage_unstable |

## Setting up a monitor

https://wiki.yandex-team.ru/geo-infra/SEDEM/

## SLA

The Ecstatic storage service has no SLA report of its own. For the time being you can refer to the 
[coordinator SLA report](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_ecstatic_coordinator)

## Logs

| Name | URL/path |
|---|---|
| Supervisord | /var/log/supervisor/* |
| Syslog | /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log |
| ymtorrent | /var/run/yandex/maps/ecstatic/ymtorrent.status |

## Release process

If you plan to rename, add, or remove a storage node, don't forget to update its record in Mongo.