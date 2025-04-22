# Maps-Core-Gpstiles-Realtime
Service for rendering realtime GPS tracks from users. Renders tiles with speed or direction information for any desired time interval during last hour.
## General information
| | |
|---|---|
| Maintainer | Ольга Заякина ( elsol@yandex-team.ru ) |
| Developers | Ольга Заякина ( elsol@yandex-team.ru ) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/gpstiles_realtime/fastcgi |
| Tracker queue | https://st.yandex-team.ru/ARMDEV |
| ABC | https://abc.yandex-team.ru/services/maps-core-gpstiles-realtime/ |
| CI | [maps-core-gpstiles-realtime](https://a.yandex-team.ru/projects/maps-core-gpstiles-realtime/ci/actions/launches?dir=maps/wikimap/gpstiles_realtime/fastcgi) |

## Instances

Nanny services

| Environment | URL | SLB | Example |
|---|---|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpstiles_realtime_stable | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-gpstiles-realtime.maps.yandex.net/show/ | https://core-gpstiles-realtime.maps.yandex.net/tiles?x=79207&y=41095&z=17&since_shift=1140&till_shift=0 |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpstiles_realtime_testing | https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-gpstiles-realtime-testing-slb | https://core-gpstiles-realtime.testing.maps.n.yandex.ru/tiles?x=79207&y=41095&z=17&since_shift=1140&till_shift=0 |
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpstiles_realtime_load | | |

## Documentation
#### Wiki description
https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/gpstilesrealtime - main page
https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/gpstilesrealtime/renderer - renderer API interaction
https://wiki.yandex-team.ru/Users/pkostikov/realtimesignalrendering/ - design review
#### Libraries and tools dev descriptions
Can be found in `readme.md` files in `tools/*`/`libs/*` subdirs.

## Known clients
https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/arm20

## What happens when service is down
Realtime gps-tracks layers (speed and directions) become unavailable

## Known issues
### Two readers with same `client_id` run simultaneously
Sympthoms:
 - significant decrease of signals count visible by clients
 - read/commit offset log messages are missing for some partitions
 - read lag is OK in LogBroker graphics (NO lag visible on graphics)
### MaxPartitions value is less than actual total partitions count
Sympthoms:
 - significant read lag present for some partitions but is missing for others
 - decrease of signals count may be visible by clients

## LogBroker read access configuration
### Topic
`maps_analyzer_tracks--analyzer-dispatcher-signals-log`
### Topic read/write configuration
https://lb.yandex-team.ru/main/topic/maps_analyzer_tracks--analyzer-dispatcher-signals-log/advanced
### Client IDs

| Environment | Client ID | Metrics URL |
|---|---|---|
| development | `maps_realtime-viewer-dev` | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer-dev/metrics |
|             | `maps_realtime-viewer-dbwriter-dev` | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer-dbwriter-dev/metrics |
| testing | `maps_realtime-viewer-tst` | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer-tst/metrics |
| stable | `maps_realtime-viewer` | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer/metrics |
| load, stress | `maps_realtime-viewer-stress` | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer-stress/metrics |

### Helpline
https://telegram.me/joinchat/BvmbJED8I3aGqqtk_ssAbg - LogBroker support
https://t.me/joinchat/AAAAAELJsROI0o5DV6mycQ - LogBroker access configuration (clients, quotas) and LogFeller support

## Monitorings
| Type | URL |
|---|---|
| Juggler (stable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_realtime_stable&view=tiles |
| Juggler (testing) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_realtime_testing&view=tiles |

## Dashboards

| Name | URL |
|---|---|
| Yacare (stable) | https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-realtime-stable-panel-main |
| Yacare (testing) | https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-realtime-testing-panel-main |
| LogBroker (testing) | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer-tst/metrics |
| LogBroker (stable) | https://lb.yandex-team.ru/main/consumer/maps_realtime-viewer/metrics |

## Logs
| Name | URL/path |
|---|---|
| YT | YQL request: SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-05-28] WHERE tskv_format='gpstiles-realtime' |

## Regression Stress Testing Configurations
| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/NMAPS-7773 |
| Task | https://st.yandex-team.ru/ARMDEV-19 |
