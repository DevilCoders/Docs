# Maps-Core-Jams-Arm
The service is responsible for storing and editing of road closures data. It's used by experts of Yandex.Jams.
## General information
| | |
|---|---|
| Developers | https://staff.yandex-team.ru/miror |
|              | https://staff.yandex-team.ru/ponomarev |
| SRE |  |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/jams_arm2 |
| Tracker queue | https://st.yandex-team.ru/ARMDEV |
| ABC | https://abc.yandex-team.ru/services/maps-core-jams-arm/ |
| CI | [maps-core-jams-arm](https://a.yandex-team.ru/projects/maps-core-jams-arm/ci/actions/launches?dir=maps/wikimap/jams_arm2/fastcgi) |

## Instances

Nanny services

| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_arm_stable |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_arm_testing |
| unstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_arm_unstable |
| dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_jams_arm/ |

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [maps-core-jams-arm.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/maps-core-jams-arm.maps.yandex.net/) | [maps-core-jams-arm.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=maps-core-jams-arm.maps.yandex.net;prj=core-jams-arm-maps;signal=service_total;) | [rtc_balancer_core-jams-arm_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-arm_maps_yandex_net_sas) <br>[rtc_balancer_core-jams-arm_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-arm_maps_yandex_net_vla) |
| Testing | common_default | [core-jams-arm.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-jams-arm.common.testing.maps.yandex.net"}) | [core-jams-arm.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-jams-arm_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |
| Unstable | common_default | [core-jams-arm.common.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.unstable.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-jams-arm.common.unstable.maps.yandex.net"}) | [core-jams-arm.common.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.unstable.maps.yandex.net;prj=common.unstable.maps.yandex.net;signal=core-jams-arm_common_unstable_maps_yandex_net;) | [rtc_balancer_common_unstable_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_sas) <br>[rtc_balancer_common_unstable_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_man) <br>[rtc_balancer_common_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_vla) |

Urls:

| Environment | URL |
|---|---|
| stable | http://maps-core-jams-arm.maps.yandex.net/closure_templates?uid=83229408 |
| testing | https://core-jams-arm.common.testing.maps.yandex.net/closure_templates?uid=83229408 |
| unstable | https://core-jams-arm.common.unstable.maps.yandex.net/closure_templates?uid=83229408 |

## Network

| Environment | Macros |
|---|---|
| stable | [MAPS_CORE_JAMS_ARM_STABLE_RTC_NETS](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_ARM_STABLE_RTC_NETS_) |
| testing, unstable | [MAPS_CORE_JAMS_ARM_TESTING_RTC_NETS](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_ARM_TESTING_RTC_NETS_) |

## Firewall

Stable:
- [UI -> backend balancer](https://puncher.yandex-team.ru/tasks?id=5af4461ed89cb016bb7d3a31)
- [tmp ARM1.0 backend -> ARM2.0 backend balancer](https://puncher.yandex-team.ru/?id=5b05baabd89cb012a2df4d69)
- backend -> dbaas: pgaas.mail.yandex.net:12000
- backend -> infopoints.maps.yandex.net:80

Testing, unstable:
- backend -> dbaas: pgaas-test.mail.yandex.net:12000
- backend -> infopoints.tst.maps.yandex.ru:80

## DBaas

[Task for quota](https://st.yandex-team.ru/MDB-2651)
projectId: 5b4e27fc-7622-4785-ac7b-885e7cf3b4b5

#### Production
clusterId: af45ea8f-6c65-4e99-ad56-1b435e7ecc2a
instance type: nano

#### Testing
clusterId: 300f758f-663b-4939-9a01-5bc73e63cfa3
instance type: nano

#### Unstable
clusterId: 17691989-694d-4c37-9f9a-cad9ede63dca
instance type: nano

#### Default settings changes
> yc mdb cluster AddExtension --name postgis --clusterId <clusterId>
> yc mdb cluster UpdateOptions --clusterId b795fc21-2631-49e7-9bb8-385765bf00fe --databaseOptions '{"pooler": {"pool_mode": "session"}}'
> yc mdb cluster UpdateUser --clusterId af45ea8f-6c65-4e99-ad56-1b435e7ecc2a --name arm --options '{"conn_limit": 50}'

#### Quick howto and links
[DBaas public docs](https://doc.yandex-team.ru/cloud/mdb/)
Use CLI for PGaaS. Up to date [docs](https://wiki.yandex-team.ru/dbaas/quickstart/#cli)
It's much more convenient than naked HTTP API.

Authorization hints
1. Get OAuth token
2. Exchange it for X-YaCloud-SubjectToken
[More about authorization](https://wiki.yandex-team.ru/dbaas/api/#autentifikacijaiavtorizacija)

DBaas project id is available [here](http://iam.cloud.yandex.net:4222/v1/mapping/abc/services/2403)

Project overview
> yc mdb cluster List --projectId=<projectId>

Quota
> yc mdb cluster GetQuota --projectId=<projectId>

#### Howto start dev DB instance

> sudo docker run -p 12101:12000 -e OPT_pre_sql='CREATE EXTENSION postgis' -e OPT_db_user=arm -e OPT_db_passwd=arm -e OPT_db_name=arm -t -d -i registry.yandex.net/dbaas/minipgaas-postgis

In case of authorization issues take a look at [docs](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija)

## Documentation
[Main page](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/arm20/)
[Deployment](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/arm20/deploy/)

## Known clients

Handlers for fetching and manipulation with objects like road events or closure templates are only used in service UI
- [UI stable](https://points.maps.yandex.ru/)
- [UI testing](https://jamsarm.tst.c.maps.yandex.ru/)

Export handlers provide complete information about current and future closures. They are used by several clients:
- router
- commercial router
- at maps.yandex.ru for closures landing https://st.yandex-team.ru/WGD-104
- at yandex.ru for displaying future drawbridges https://st.yandex-team.ru/HOME-43444

## Ecstatic Datasets
- yandex-maps-coverage5-geoid
- yandex-maps-coverage5-trf
- yandex-maps-geobase-tzdata
- yandex-maps-geodata6
- yandex-maps-graph-closures
- yandex-maps-masstransit-closures-src
- yandex-maps-graph-activator
- yandex-maps-graph-compact
- yandex-maps-graph-compact-edges-persistent-index
- yandex-maps-graph-compact-rtree
- yandex-maps-graph-router-compact-data7
- yandex-maps-graph-router-topology7

## What happens when service is down
Both routers commercial and regular navigate throw known road closures.

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


### Helpline
Infopoints aggregator: ask aeol@
DBaas: tg chat - https://t.me/joinchat/AAAAAEDje_JvGnMnVZxVvA
RTC: tg chat - https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q


## Dashboards

| Name | URL |
|---|---|
| Yacare stable (by sedem)| https://yasm.yandex-team.ru/template/panel/maps-core-jams-arm-stable-panel-main |
| Yacare testing (by sedem)| https://yasm.yandex-team.ru/template/panel/maps-core-jams-arm-testing-panel-main |
| Yacare unstable (by sedem)| https://yasm.yandex-team.ru/template/panel/maps-core-jams-arm-unstable-panel-main |
| DBaas stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=af45ea8f-6c65-4e99-ad56-1b435e7ecc2a;dbname=maps_core_jams_arm |
| DBaas testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=300f758f-663b-4939-9a01-5bc73e63cfa3;dbname=maps_core_jams_arm_testing |
| DBaas unstable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=17691989-694d-4c37-9f9a-cad9ede63dca;dbname=maps_core_jams_arm_dev |

## Monitorings

| Name | URL |
|---|---|
| Juggler stable (by sedem) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_arm_stable&view=tiles |
| Juggler testing (by sedem) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_arm_testing&view=tiles |
| Juggler unstable (by sedem) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_arm_unstable&view=tiles |

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| JamsArm | /var/log/yandex/maps/jams-arm/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | YQL request: SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-05-28] WHERE tskv_format='jams-arm' |
| DBaas | yc mdb cluster GetLogs --clusterId=af45ea8f-6c65-4e99-ad56-1b435e7ecc2a --service postgres --columns "ms,query,user_name" --fromTime -3600 --toTime -0 |

## SLA
Absent

## Regression Stress Testing Configurations
No more than 10 users are using this service. No need in regression test performing.
