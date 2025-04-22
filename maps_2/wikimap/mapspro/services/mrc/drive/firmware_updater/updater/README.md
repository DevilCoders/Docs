# Maps Core Firmware Updater


## General information
| What | Who |
| ---- | --- |
| Responsible | Konstantin Tesker (k-tesker@yandex-team.ru)|
| Responsible SRE | Konstantin Tesker (k-tesker@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/drive/firmware_updater/updater |
| ABC service | https://abc.yandex-team.ru/services/maps-core-firmware-updater |

## Service infrastructure
### Instances, graphics, monitorings
| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_firmware_updater_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_firmware_updater_stable/) | [core-firmware-updater.stable](https://yasm.yandex-team.ru/template/panel/maps-core-firmware-updater-stable-panel-main/) | [maps_core_firmware_updater_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_firmware_updater_stable) |
| Testing | [maps_core_firmware_updater_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_firmware_updater_testing/) | [core-firmware-updater.testing](https://yasm.yandex-team.ru/template/panel/maps-core-firmware-updater-testing-panel-main/) | [maps_core_firmware_updater_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_firmware_updater_testing) |
[Monitorings all (tag=a_prj_maps-core-firmware-updater)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-firmware-updater)

### Balancers
| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-firmware-updater.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-firmware-updater.maps.yandex.net/) | [core-firmware-updater.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-firmware-updater.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-firmware-updater-maps;signal=service_total) | [rtc_balancer_core-firmware-updater_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-updater_maps_yandex_net_man)<br>[rtc_balancer_core-firmware-updater_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-updater_maps_yandex_net_sas)<br>[rtc_balancer_core-firmware-updater_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-updater_maps_yandex_net_vla) |
| Testing | Default | [core-firmware-updater.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-firmware-updater.testing.maps.yandex.net/) | [core-firmware-updater.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-firmware-updater.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-firmware-updater-testing-maps;signal=service_total) | [rtc_balancer_core-firmware-updater_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-updater_testing_maps_yandex_net_sas) |


### Racktables network macros
- Stable: https://racktables.yandex-team.ru/index.php?page=file&file_id=2847467
- Testing: https://racktables.yandex-team.ru/index.php?page=file&file_id=2847466


## Documentation
https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/drive/firmware_updater/README-proposal.md


## What happens when service is down
- It is not possible for clients to update firmware.


## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Fastcgi | /var/log/yandex/maps/firmware-updater/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : select * from hahn.[home/logfeller/logs/maps-log/1d/2018-02-28] where tskv_format='firmware-updater' |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Persistent Volumes
/logs - symlink from /var/log
