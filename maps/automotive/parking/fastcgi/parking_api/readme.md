## General information
Service registers yandex.auto HU users, sends parking push notifications using XIVA and works with parking sessions (get active, stop)

| What | Who |
| ---- | --- |
| Responsible SE | Roman Peshkurov (peshkurov@yandex-team.ru) |
| Responsible SRE | Mikhail Krutyakov (mkrutyakov@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_api |
| ABC-service | https://abc.yandex-team.ru/services/maps-auto-parking-api/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_PARKING_API |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Testing | [maps_auto_parking_api_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_testing/) | [ auto-parking-api.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-api-testing-panel-main/) | [ maps_auto_parking_api_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_api_testing) |
| Prestable | [maps_auto_parking_api_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_prestable/) | [ auto-parking-api.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-api-prestable-panel-main/) | [ maps_auto_parking_api_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_api_prestable) |
| Stable | [maps_auto_parking_api_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_stable/) | [ auto-parking-api.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-api-stable-panel-main/) | [ maps_auto_parking_api_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_api_stable) |
| Stress | [maps_auto_parking_api_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_stress/) | [ auto-parking-api.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-parking-api-stress-panel-main/) | [ maps_auto_parking_api_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_parking_api_stress) |
[Monitorings all (tag=a_prj_maps-auto-parking-api)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-parking-api) <br>
[Metrics dashboard](https://yasm.yandex-team.ru/panel/dtyo._VNSCu8/)

## Balancers
| Testing | URL |
|---|---|---|
| l3-балансер | https://l3.tt.yandex-team.ru/service/7347 |
| l3-балансер в racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=8529 |
| awacs-l3-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-api.testing.maps.yandex.net/l3-balancers/list/ |
| awacs-l7-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-api.testing.maps.yandex.net/show/ |
| nanny-сервисы для awacs-l7-балансеров | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-api_testing_maps_yandex_net_sas/ |

| Stable | URL |
| ------ | --- |
| l3-балансер | https://l3.tt.yandex-team.ru/service/7482 |
| l3-балансер в racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=8881 |
| awacs-l3-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-api.maps.yandex.net/l3-balancers/list/auto-parking-api.maps.yandex.net/show/ |
| awacs-l7-балансер | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-parking-api.maps.yandex.net/show/ |
| nanny-сервисы для awacs-l7-балансеров | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-api_maps_yandex_net_sas/<br> https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-api_maps_yandex_net_vla/<br> https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-parking-api_maps_yandex_net_man/ |


## What happens when service is down

When the service is down head units won't be registered and parking notifications won't be sent to users' devices.

## Ecstatic dataset

yandex-maps-carparks-handler-data

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-parking-api/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : USE hahn; SELECT * FROM `logs/maps-log/1d/2020-03-02` WHERE vhost='auto-parking-api.maps.yandex.net'; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Check a log `/logs/yandex/maps/auto-parking-api/auto-parking-api.log`. Most probably you'll find some tips about what is going wrong. There are few things that could go wrong.
If the log shows that some forwarding register_device requests failed, then you should check Nanny if all of parking api instances are active.
If there are some problems with Yandex.Money or XIVA (sendPush failed), contact responsible of corresponding service.

## Documentation

https://wiki.yandex-team.ru/automotive/serverdevelopment/projects/parkingv2/ <br>
https://wiki.yandex-team.ru/automotive/serverdevelopment/projects/parkingv2/architectural/

## Known clients

## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_auto_parking_api) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_auto_parking_api.py)

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_parking_api_stress/yp_pods/ |


## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_PARKING_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PARKING_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_PARKING_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PARKING_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
| Type | URL |
|---|---|
| Sandbox scheduler for regular stress testing with constant rps | https://sandbox.yandex-team.ru/scheduler/19147/view |
| Sandbox scheduler for regular stress testing with linear rps | https://sandbox.yandex-team.ru/scheduler/19146/view |
| Tracker ticket for constant rps | https://st.yandex-team.ru/YCARBACKEND-340 |
| Tracker ticket for linear rps | https://st.yandex-team.ru/YCARBACKEND-341 |
| CI | https://lunapark.yandex-team.ru/regress/YCARBACKEND |

## Release Machine

It's preferable to use console commands to be able to track changes history.
```
$ ya tool sedem release info maps/automotive/parking/fastcgi/parking_api
$ ya tool sedem release start maps/automotive/parking/fastcgi/parking_api //create new relase
$ ya tool sedem release step maps/automotive/parking/fastcgi/parking_api $VERSION $STAGING
```

Release machine UI https://rm.z.yandex-team.ru/component/maps_auto_parking_api


## TVM id
| Staging | ID |
| ------- | -- |
| stable | 2015423 |
| testing | 2015421 |
| stress | 2017411 |

## API
All requests MUST contain params:
- uuid
- lang
- device_id

All methods can return:
- HTTP 200 (OK)
- HTTP 400 (Bad Request) - client error, incorrect query params
- HTTP 401 (Unauthorized) - authorization header is missing or contains invalid token
- HTTP 422 (Logic Error) - request should not be retried with the same params values
- HTTP 5xx (Server Error) - request should be retried

### /parking/1.x/active_sessions
Get user active parking sessions
| Method | GET |
| ------ | --- |
| **Params**   |
| device_id | head unit device id |
|              |
| **Headers**  |
| Authorization | contains OAuth $token |


### /parking/1.x/stop_session
Stop parking session with given ID

| Method | POST |
| ------ | ---- |
| **Params**        |
| session_id | [required] session id |
|                            |
| **Headers**                |
| Authorization | contains OAuth $token |


### /parking/1.x/register_device
Link user UID with device DEVICE_ID

| Method | POST |
| ------ | ---- |
| **Params**    |
| device_id | head unit device id |
|                                 |
| **Headers**                     |
| Authorization | contains OAuth $token |

## Internal API

### /parking/1.x/internal/register_devices
Method for syncing device_id - uid pairs between servers

| Method | POST |
| ------ | ---- |
| **Body** | protobuf with device_id - uid pairs |
[parking_internal.proto](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/proto/parking_internal.proto)


### /parking/1.x/internal/check_parking
Check and send push about parking to the stopped user if necessary.
| Method | POST |
| ------ | ---- |
| **Params**    |
| device_id | head unit device id |
| ll        | coordinates of head unit stop (lat, lon) |
