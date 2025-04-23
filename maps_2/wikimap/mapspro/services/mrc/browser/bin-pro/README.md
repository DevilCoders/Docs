# MRC Browser Pro

Бэкенд для просмотра скрытых фотографий, доступ только из внутренней сети
Backend for hidden mrc photos, access from internal network only

## General information
| Key | Value |
| --- | ----- |
| Responsible | [Mikhail Plotkin](https://staff.yandex-team.ru/miplot) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/bin-pro |
| ABC service | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-browser-pro |
| CI Testenv per commit build task | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_BROWSER_PRO |

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Datatesting | [maps_core_nmaps_mrc_browser_pro_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_pro_datatesting/) | [ core-nmaps-mrc-browser-pro.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-pro-datatesting-panel-main/) | [ maps_core_nmaps_mrc_browser_pro_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_pro_datatesting) |
| Stable | [maps_core_nmaps_mrc_browser_pro_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_pro_stable/) | [ core-nmaps-mrc-browser-pro.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-pro-stable-panel-main/) | [ maps_core_nmaps_mrc_browser_pro_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_pro_stable) |
| Testing | [maps_core_nmaps_mrc_browser_pro_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_pro_testing/) | [ core-nmaps-mrc-browser-pro.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-pro-testing-panel-main/) | [ maps_core_nmaps_mrc_browser_pro_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_pro_testing) |

[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-browser-pro)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-browser-pro)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-mrc-browser-pro.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-browser-pro.maps.yandex.net/) | [core-nmaps-mrc-browser-pro.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-mrc-browser-pro.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-nmaps-mrc-browser-pro-maps;signal=service_total) | [rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser-pro_maps_yandex_net_vla) |
| Testing |  | [nmaps-mrc-pro-testing.tst.c.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-nmaps-mrc-browser-pro.common.testing.maps.yandex.ru_default/show/) |[nmaps-mrc-pro-testing.tst.c.maps.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=common.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=common.testing.maps.yandex.net;signal=core-nmaps-mrc-browser-pro_common_testing_maps_yandex_ru) | |
| Datatesting | | [nmaps-mrc-pro-datatesting.tst.c.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list/core-nmaps-mrc-browser-pro.common.datatesting.maps.yandex.ru_default/show/) | [nmaps-mrc-pro-datatesting.tst.c.maps.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=common.datatesting.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=common.datatesting.maps.yandex.net;signal=core-nmaps-mrc-browser-pro_common_datatesting_maps_yandex_ru;) | | 

## Documentation

Fixme: add separate doc page for browser pro
https://wiki.yandex-team.ru/jandekskarty/projects/catalog/ek/ek-nk/projects/automnyak/main/mrc-browser-api/


## Known clients

Layer of MRC photos in NMAPS:
| Environment | URL |
| ----------- | --- |
| Production | [npro.maps.yandex.ru](https://npro.maps.yandex.ru) |
| Testing | [nmaps-mrc-pro-testing.tst.c.maps.yandex.ru](https://nmaps-mrc-pro-testing.tst.c.maps.yandex.ru) |
| Datatesting | [nmaps-mrc-pro-datatesting.tst.c.maps.yandex.ru](https://nmaps-mrc-pro-datatesting.tst.c.maps.yandex.ru) | 


## What happens when service is down

Hidden photos in private regions will not load. Hidden photos are for internal use only.


## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Racktables network macros

| Environment | Macros |
| ----------- | ------ |
| Stable | [MAPS_CORE_NMAPS_MRC_BROWSER_PRO_STABLE_RTC_NETS](https://racktables.yandex-team.ru/index.php?file_id=2841086&page=file&tab=default) |
| Testing | [MAPS_CORE_NMAPS_MRC_BROWSER_PRO_TESTING_RTC_NETS](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2841085) |


## Ecstatic Datasets
| Stable | Testing | Datatesting |
| ------ | ------- | ----------- |
| [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) |
| [yandex-maps-mrc-activation](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) | [yandex-maps-mrc-activation](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) | [yandex-maps-mrc-activation](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) |
| [yandex-maps-mrc-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) | [yandex-maps-mrc-graph-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) | [yandex-maps-mrc-graph-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) |
| [yandex-maps-mrc-pedestrian-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) | [yandex-maps-mrc-pedestrian-graph-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) | [yandex-maps-mrc-pedestrian-graph-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) |
| [yandex-maps-mrc-photo-to-edge-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge-pro/versions) | [yandex-maps-mrc-photo-to-edge-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge-pro/versions) | [yandex-maps-mrc-photo-to-edge-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge-pro/versions) |
| [yandex-maps-mrc-photo-to-pedestrian-edge-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge-pro/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge-pro/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge-pro/versions) |
| [yandex-maps-mrc-design](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) | [yandex-maps-mrc-design](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) | [yandex-maps-mrc-design](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) |

## Logs

Logs can be found in Nanny container instances by following paths:

| Name | Path |
| ---- | ---- |
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Fastcgi | /var/log/yandex/maps/mrc-browser-pro/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

### Logs in YT
https://yql.yandex-team.ru
```sql
select * from hahn.`//home/logfeller/logs/maps-log/1d/2021-04-19`  where tskv_format='mrc-browser-pro'
```
