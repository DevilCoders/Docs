# Maps-Core-Gpsrealtime-Hypgen
The service generates hypotheses about road closures based on realtime GPS signals.

## General information

| Key | Value |
|---|---|
| Developer | https://staff.yandex-team.ru/ponomarev, https://staff.yandex-team.ru/chikunov |
| SRE | https://staff.yandex-team.ru/ponomarev |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/gpsrealtime_hypgen |
| Tracker queue | https://st.yandex-team.ru/ARMDEV |
| ABC | https://abc.yandex-team.ru/services/maps-core-gpsrealtime-hypgen/ |
| CI | [maps-core-gpsrealtime-hypgen](https://a.yandex-team.ru/projects/maps-core-gpsrealtime-hypgen/ci/actions/launches?dir=maps/wikimap/gpsrealtime_hypgen/fastcgi) |

## Instances

Nanny services

| Environment | URL |
|---|---|
| dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_gpsrealtime_hypgen/ |
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpsrealtime_hypgen_stable |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpsrealtime_hypgen_testing |

## DBaas

[Task for quota](https://st.yandex-team.ru/MDBSUPPORT-737)
projectId: 6cc1babe-8371-4a00-b544-2a60e63fc3d0

#### Production
clusterId: 9665b96e-fad2-49c4-962e-8ab7df9d8280
instance type: micro

#### Testing
clusterId: bd4f7d6a-c291-4e06-bc0d-f1860e390474
instance type: nano

#### Default settings changes
> yc mdb cluster AddExtension --name postgis --clusterId <clusterId>
> yc mdb cluster UpdateOptions --clusterId b795fc21-2631-49e7-9bb8-385765bf00fe --databaseOptions '{"pooler": {"pool_mode": "session"}}'

## Documentation
https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/gpsrealtime-hypgen/

## Known clients
[ARM2.0](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/arm20)

## What happens when service is down
No GPS signals based hypotheses about road closures are generated.

## Ecstatic Datasets
- yandex-maps-geodata6
- yandex-maps-graph-activator
- yandex-maps-graph-compact-edges-persistent-index
- yandex-maps-graph-compact-rtree
- yandex-maps-graph-data
- yandex-maps-graph-edges-persistent-index
- yandex-maps-graph-topology
- yandex-maps-jams-speeds

## Monitorings

| Name | URL |
|---|---|
| Juggler stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpsrealtime_hypgen_stable&limit=40&view=tiles |
| Juggler testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpsrealtime_hypgen_testing&limit=40&view=tiles |

## Dashboards

| Name | URL |
|---|---|
| Yacare stable | https://yasm.yandex-team.ru/template/panel/maps-core-gpsrealtime-hypgen-stable-panel-main |
| Yacare testing | https://yasm.yandex-team.ru/template/panel/maps-core-gpsrealtime-hypgen-testing-panel-main |
| DBaas stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=9665b96e-fad2-49c4-962e-8ab7df9d8280;dbname=hypgen |
| DBaas testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=bd4f7d6a-c291-4e06-bc0d-f1860e390474;dbname=hypgen_testing |

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Gpsrealtime_hypgen | /var/log/yandex/maps/gpsrealtime_hypgen/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | YQL request: SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-05-28] WHERE tskv_format='gpsrealtime_hypgen' |

## SLA
Absent

## Regression Stress Testing Configurations
Only statistics is provided by HTTP-requests. No need of regression tests.