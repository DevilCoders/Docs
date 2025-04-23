# Maps-Auto-Updater

Calculates updates info for automotive head units.

## General information

| Key | Value |
|---|---|
| Responsible SE & SRE | https://staff.yandex-team.ru/4c4d <br/> https://staff.yandex-team.ru/oklimin |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/updater |
| ABC-service | https://abc.yandex-team.ru/services/maps-auto-updater/ |
| Tracker Queue | https://st.yandex-team.ru/YCARBACKEND |
| Tanker | https://tanker.yandex-team.ru/?project=yandexauto&branch=master |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_UPDATER|

## Instances

| Environment | URL |
|---|---|
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_updater_stable|
| Prestable |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_updater_prestable|
| Testing |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_updater_testing|
| Stress |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_updater_stress|
| Dashboard |https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_auto_updater/|

## Documentation
https://wiki.yandex-team.ru/Automotive/serverdevelopment/auto-updater/devops/<br>
https://wiki.yandex-team.ru/Automotive/serverdevelopment/auto-updater/architectural/


## What happens when service is down
Head units won't receive software updates as if there weren't any.<br>
Sample queries to check if updater works:
(testing)
```
curl "https://auto-updater.tst.maps.yandex.net/updater/1.x/updates?lang=ru_RU&type=carsharing&vendor=kia&model=rio&mcu=microntek_n&uuid=251623cff3ff5de96c2f69d4497063d6" --data '[{"package":"ru.yandex.yandexnavi","version":{"code":1,"text":"1.0"}},{"package":"yandex.auto","version":{"code":0,"text":"0.0"}}]'

```
(stable)
```
curl "https://automotive.yandex.net/updater/1.x/updates?lang=ru_RU&type=carsharing&vendor=kia&model=rio&mcu=microntek_n&uuid=251623cff3ff5de96c2f69d4497063d6" --data '[{"package":"ru.yandex.yandexnavi","version":{"code":1,"text":"1.0"}},{"package":"yandex.auto","version":{"code":0,"text":"0.0"}}]'

```
Check if beta.m.ya.ru updater works:
```
curl "https://updater.mobile.yandex.net/api/v1/updates?locale=ru_RU" -H "User-Agent: com.yandex.launcher.updaterapp/1.2.8 (rockchip d200; Android 4.4.2)"  -H "X-YaUuid: 2516d3cff3ff5de96c2f69d4497063d6" -H 'X-Updr-Tags: autolauncher,release,carsharing,astar,RU' | json_pp
```


## How to fix common problems
###HTTP 400 and HTTP 422 codes
These codes are quite common, HTTP 422 is reserved for unknown head unit types.<br>
If you are on duty and HTTP 4xx monitoring triggers, set downtime and create a ticket in YCARBACKEND queue to check logs for unknown head unit types.

###Cache age
The service uses beta.m.ya.ru storage for .apk, sometimes it's down and we are not able to update packages versions cache.<br>
Check if it works with the query above or try ssh an updater instance and update cache manually:
```
curl -v6 -H "Host: updater.automotive.yandex.net" localhost/update-cache
```
If it's still not working and it's down for more than 24hrs, call stef@ or kindrik@ to fix it.



## SLA
| | URL |
|---|---|
|Отчёт | https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_auto_updater |

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dauto-updater-alive&view=tiles |


## Balancers

| Stable | URL |
|---|---|
| l3-balancer | https://l3.tt.yandex-team.ru/service/5746 |
| l3-balancer (racktables) | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=7128 |
| awacs-l3-balancer | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-updater.maps.yandex.net/l3-balancers/list/ |
| awacs-l7-balancer | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-updater.maps.yandex.net/show/ |
| nanny-services for awacs-l7-balancers | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_maps_yandex_net_man/ |
| | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_maps_yandex_net_sas/ |
| | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_maps_yandex_net_vla/ |


| Testing | URL |
|---|---|
| l3-balancer | https://l3.tt.yandex-team.ru/service/5726 |
| l3-balancer (racktables) | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=7108 |
| awacs-l3-balancer | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-updater.testing.maps.yandex.net/l3-balancers/list/ |
| awacs-l7-balancer | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-updater.testing.maps.yandex.net/show/ |
| nanny-services for awacs-l7-balancers | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_testing_maps_yandex_net_man/ |
| | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_testing_maps_yandex_net_sas/ |
| | https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-updater_testing_maps_yandex_net_vla/ |


## Logs

| Name | URL/path |
|---|---|
| nginx | `/var/log/nginx/` |
| roquefort | `/var/log/yandex/maps/roquefort/` |
| yacare | `/var/log/yandex/maps/yacare/` |
| auto-updater | `/var/log/yandex/maps/auto-updater/` |
| supervisord | `/var/log/supervisor/` |
| syslog (unfiltered) | `/var/log/syslog` |
| juggler | `/juggler/logs/` |
| [YT](https://yql.yandex-team.ru)  | `SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2019-06-24] WHERE tskv_format = 'auto-updater'` |
| YT verbose (testing) | [//home/logfeller/logs/maps-auto-updater-testing-logs/](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-auto-updater-testing-logs) |
| YT verbose (stable) | [//home/logfeller/logs/maps-auto-updater-stable-logs/](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-auto-updater-stable-logs) |


## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Sandbox scheduler for regular stress testing with constant rps | https://sandbox.yandex-team.ru/scheduler/19258 |
| Sandbox scheduler for regular stress testing with linear rps | https://sandbox.yandex-team.ru/scheduler/19259 |
| Tracker ticket for constant rps | https://lunapark.yandex-team.ru/YCARBACKEND-51 |
| Tracker ticket for linear rps | https://lunapark.yandex-team.ru/YCARBACKEND-52 |
| CI | https://lunapark.yandex-team.ru/regress/YCARBACKEND |


## SECAUDIT

https://st.yandex-team.ru/SECAUDIT-2238


## Yasm dashboard

| Name | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/panel/beaver._eU5Pdc/ |
| Traffic (S3) | https://yasm.yandex-team.ru/template/panel/s3_mds_nginx/bucket=maps-auto-store-internal/?range=5184000000 |


## SEDEM dashboards for yasm
| url |
|---|
| https://yasm.yandex-team.ru/template/panel/maps-auto-updater-prestable-panel-main/ |
| https://yasm.yandex-team.ru/template/panel/maps-auto-updater-stress-panel-main/ |
| https://yasm.yandex-team.ru/template/panel/maps-auto-updater-stable-panel-main/ |
| https://yasm.yandex-team.ru/template/panel/maps-auto-updater-testing-panel-main/ |


## Release Machine
It preferable to use console commands to be able to track changes history.
```
$ ya tool sedem release info maps/automotive/updater
$ ya tool sedem release start maps/automotive/updater //create new relase
$ ya tool sedem release step maps/automotive/updater $VERSION $STAGING
```

Release machine UI https://rm.z.yandex-team.ru/component/maps_auto_updater


## Logbroker

Topics:

```$ logbroker -s logbroker.yandex.net schema list /maps-auto-updater```


## Logfeller

At the moment there are two logs configured at cluster Hahn:
- maps-auto-updater-testing-logs
- maps-auto-updater-stable-logs

The actual configuration can be found here:
https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/common_hahn_logs.json

Solomon dashboards:

| Environment | URL |
|-|-|
| Testing | https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=maps-auto-updater%40testing-logs |
| Stable  | https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=maps-auto-updater%40stable-logs  |
