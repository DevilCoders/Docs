# Auto Parking Receiver

Processing GPS and CAN signals from cars with Yandex.Auto onboard and detecting if car was parked

## General information
| What | Who |
| ---- | --- |
| Responsible SE | Roman Peshkurov (peshkurov@yandex-team.ru) |
| Responsible SRE | Mikhail Krutyakov (mkrutyakov@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_receiver |
| ABC-service | https://abc.yandex-team.ru/services/maps-auto-parking-receiver/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_PARKING_RECEIVER |

## Tips & tricks
To run locally
ya make -DCFLAGS="-DMOCK_YACARE_USER_ID"
./run.sh

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Testing | [maps_auto_parking_receiver_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_testing/) | [ auto-parking-receiver.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-receiver-testing-panel-main/) | [ maps_auto_parking_receiver_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_receiver_testing) |
| Stress | [maps_auto_parking_receiver_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_stress/) | [ auto-parking-receiver.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-receiver-stress-panel-main/) | [ maps_auto_parking_receiver_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_receiver_stress) |
| Prestable | [maps_auto_parking_receiver_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_prestable/) | [ auto-parking-receiver.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-receiver-prestable-panel-main/) | [ maps_auto_parking_receiver_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_receiver_prestable) |
| Stable | [maps_auto_parking_receiver_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_stable/) | [ auto-parking-receiver.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-receiver-stable-panel-main/) | [ maps_auto_parking_receiver_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_receiver_stable) |
[Monitorings all (tag=a_prj_maps-auto-parking-receiver)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-parking-receiver)

- https://charts.yandex-team.ru/preview/hy7uiu999t8ad - a chart on number of cars with CAN sensors available 
- https://sandbox.yandex-team.ru/scheduler/23654/view - scheduler 

## Balancers
| Staging | Name | URL |
|---|---|---|
| Testing | awacs-l7-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-receiver.testing.maps.yandex.net/show/ |
| Testing | nanny-сервисы для awacs-l7-балансеров | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-receiver_testing_maps_yandex_net_sas/ |
| Stable | awacs-l7-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-receiver.maps.yandex.net/show/ |
| Stable | nanny-сервисы для awacs-l7-балансеров | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-receiver_maps_yandex_net_man/<br> https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-receiver_maps_yandex_net_sas/<br> https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-receiver_maps_yandex_net_vla/ |


## MongoDB Cluster

We have two clusters of 3 nodes each, one is for stable environment,
the second one is for testing and development. 
[Stable YC cluster](https://yc.yandex-team.ru/folders/foo1cm95m01h18apeckk/managed-mongodb/cluster/mdbd6sehbq7gakqu2ht7)
[Testing YC cluster](https://yc.yandex-team.ru/folders/foo1cm95m01h18apeckk/managed-mongodb/cluster/mdb8gdv39nge942u6joo)

## What happens when service is down

When the service is down a parking detection routine won't work, so a user came to paid parking won't receive push message
with parking number.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-parking-receiver/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : USE hahn; SELECT * FROM `logs/maps-log/1d/2020-03-02` WHERE vhost='auto-parking-receiver.maps.yandex.net'; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Check a log `/logs/yandex/maps/auto-parking-receiver/auto-parking-receiver.log`. Most probably you'll find some tips about what is going wrong.
If it says that check parking request failed, something went wrong in auto-parking-api and you need to investigate problem [there](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_api#what-happens-when-service-is-down).
If it says that there are some problems with updating/finding vehicle data the problem most likely is in mongo storage, so check if it's alive [here](https://yc.yandex-team.ru/folders/foo1cm95m01h18apeckk/managed-mongodb/cluster/mdbd6sehbq7gakqu2ht7).

## Documentation

https://wiki.yandex-team.ru/automotive/serverdevelopment/projects/parkingv2/ <br>
https://wiki.yandex-team.ru/automotive/serverdevelopment/projects/parkingv2/architectural/

### Request processing summary

Receiver processes two kind of requests: matched path and telemetry.
Matched path is a tail of a car track attached to the edges of the road graph.
Telemetry are "raw" car hardware events obtained from CAN bus (e.g. ignition state, steering wheel angle, etc.).

For each moving car Receiver maintains a state. A state consists of latest matched path, some number of telemetry events and a calculated status. Most important part of status object is car motion state (i.e. moving, stopped, parked, etc.). Upon motion state change to "parking" Receiver initiate "check parking" call to Parking Api.

To address concurrent nature of events Receiver utilizes MongoDB cluster to serialize writes and adheres to the following update protocol.
First car state is updated with data from request. This step is "logically guaranteed" (i.e. ignoring cluster failures) to complete without conflicts with any other concurrent write. Second step is to fetch car state from database, recalculate the status and write it back (CAS operation). If status was concurrently updated by other process (i.e. CAS failed) then repeat second step until status incorporates current update. Second step is guaranteed to complete in 2 attempts (second attempt failure means that status already includes current request's update processed by other process).

Few remarks on protocol. Document consists of 3 independent parts: path, telemetry, status. Writes to particular document are serialized by MongoDB. Writes to path and telemetry doesn't require fetching data before update. Telemetry events are appended to array field. Matched path object is rewritten. In theory write to the matched path can fail if newer version is already there, but this mean that this request can be ignored completely. Status CAS operation based on telemetry version and matched path timestamp. Status is replaced if and only if document contains unchanged status since it was fetched by Receiver process.

### MongoDB database and document structure

Database consists of a single collection "telemetry". Single collection ensures "consistency" when reading data. Collection has unique index by device id and TTL index by "updated at" timestamp. TTL index is used to remove stale data (i.e. for cars that are not moving and are no interest to Receiver).

Each document has following structure:

| Field | Type | Index | Description |
|---|---|---|---|
| updated_at | Date | TTL index | Date and time when this document was last updated. Used for TTL index. Documents older that 60 minutes are removed. |
| device_id | String | Unique index | Yandex Metrica device id. Unique head-unit identifier. This field will be used for sharding in the future. |
| matched_path | Object | - |  Latest matched path for this head-unit. |
| matched_path.updated_at | long | - | Timestamp of this path. Internally this is timestamp of last GPS signal. Seconds since Epoch UTC. |
| matched_path.proto_data | binData | - | Matched path serialized protobuf message. |
| telemetry | Object | - | Telemetry events container. |
| telemetry.version | int | - | Version of telemetry object. Incremented each time telemetry event is added here. |
| telemetry.ignition | Array | - | Array of binData. Each element contain serialized CanEvent protobuf message with ignition state changes. |
| status | Object | - | Status object. |
| status.path_updated_at | long | - | Path timestamp used when this status was calculated. This field is used for optimistic locking (i.e. CAS operation). |
| status.telemetry_version | int | - | Version of telemetry used when this status was calculated. This field is used for optimistic locking (i.e. CAS operation). |
| status.state | String | - | Motion state of this head-unit. |
| status.lon | Double | - | Longitude of last known position. |
| status.lat | Double | - | Latitude of last known position. |

## Known clients


## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_auto_parking_receiver) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_auto_parking_receiver.py)


## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_receiver_stress/yp_pods/ |

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_PARKING_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PARKING_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_PARKING_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PARKING_TESTING_RTC_NETS_ ) |


## Regression Stress Testing Configurations
| Type | URL |
|---|---|
| Sandbox scheduler for regular stress testing with constant rps | https://sandbox.yandex-team.ru/scheduler/18870/view |
| Sandbox scheduler for regular stress testing with linear rps | https://sandbox.yandex-team.ru/scheduler/18727/view |
| Tracker ticket for constant rps | https://st.yandex-team.ru/YCARBACKEND-324 |
| Tracker ticket for linear rps | https://st.yandex-team.ru/YCARBACKEND-323 |
| CI | https://lunapark.yandex-team.ru/regress/YCARBACKEND |


## Release Machine

It's preferable to use console commands to be able to track changes history.
```
$ ya tool sedem release info maps/automotive/parking/fastcgi/parking_receiver
$ ya tool sedem release start maps/automotive/parking/fastcgi/parking_receiver //create new relase
$ ya tool sedem release step maps/automotive/parking/fastcgi/parking_receiver $VERSION $STAGING
```

Release machine UI https://rm.z.yandex-team.ru/component/maps_auto_parking_receiver


## Logbroker

Topics:

[stable](https://beta.lb.yandex-team.ru/logbroker/accounts/maps_auto/parking-receiver-stable-log) <br>
[testing](https://beta.lb.yandex-team.ru/logbroker/accounts/maps_auto/parking-receiver-testing-log)

```$ logbroker -s logbroker.yandex.net schema list /maps_auto```


## Logfeller

At the moment there are two logs configured at cluster Hahn:
- maps-auto-parking-receiver-testing-log
- maps-auto-parking-receiver-stable-log

The actual configuration can be found here:
https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/common_hahn_logs.json

Solomon dashboards:

| Environment | URL |
|-|-|
| Testing | https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=maps_auto-parking-receiver-testing-log |
| Stable  | https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=maps_auto-parking-receiver-stable-log |


## TVM id
| Staging | ID |
| ------- | -- |
| stable | 2015825 |
| testing | 2015823 |

## API
All requests MUST contain params:
- uuid
- device_id

### /datacollect/1.x/matched_path
Collect matched path and check parking state

| Method | POST |
| ------ | ---- |
| **Params**    |
| clid |  |
| uuid |  |
| device_id | head unit device id |
| **Body** | protobuf with MatchedPath |
[matched_path.proto](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/matcher/matched_path.proto)

### /datacollect/1.x/vehicle_data
Collect CAN data and check parking state

| Method | POST |
| ------ | ---- |
| **Params**    |
| device_id | head unit device id |
| **Body** | protobuf with CarEvent |
[telemetry.proto](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/proto/datacollect/telemetry.proto)
