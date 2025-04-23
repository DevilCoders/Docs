# Maps Core Firmware Storage


## General information
| What | Who |
| ---- | --- |
| Responsible | Mikhail Plotkin (miplot@yandex-team.ru)|
| Responsible SRE | Mikhail Plotkin (miplot@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/drive/firmware_updater/storage |
| ABC service | https://abc.yandex-team.ru/services/maps-core-firmware-storage |

## Service infrastructure
### Instances, graphics, monitorings
| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_firmware_storage_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_firmware_storage_stable/) | [core-firmware-storage.stable](https://yasm.yandex-team.ru/template/panel/maps-core-firmware-storage-stable-panel-main/) | [maps_core_firmware_storage_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_firmware_storage_stable) |
| Testing | [maps_core_firmware_storage_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_firmware_storage_testing/) | [core-firmware-storage.testing](https://yasm.yandex-team.ru/template/panel/maps-core-firmware-storage-testing-panel-main/) | [maps_core_firmware_storage_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_firmware_storage_testing) |
[Monitorings all (tag=a_prj_maps-core-firmware-storage)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-firmware-storage)

### Balancers
| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-firmware-storage.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-firmware-storage.maps.yandex.net/) | [core-firmware-storage.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-firmware-storage.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-firmware-storage-maps;signal=service_total) | [rtc_balancer_core-firmware-storage_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-storage_maps_yandex_net_man)<br>[rtc_balancer_core-firmware-storage_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-storage_maps_yandex_net_sas)<br>[rtc_balancer_core-firmware-storage_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-storage_maps_yandex_net_vla) |
| Testing | Default | [core-firmware-storage.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-firmware-storage.testing.maps.yandex.net/) | [core-firmware-storage.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-firmware-storage.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-firmware-storage-testing-maps;signal=service_total) | [rtc_balancer_core-firmware-storage_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-firmware-storage_testing_maps_yandex_net_sas) |


### Racktables network macros
- Stable: https://racktables.yandex-team.ru/index.php?page=file&file_id=2847448
- Testing: https://racktables.yandex-team.ru/index.php?page=file&file_id=2847447


## Documentation
https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/drive/updater/README-proposal.md


## Known clients
IDM. Both stable and testing stagings are integrated with production IDM.
- Stable: https://idm.yandex-team.ru/system/maps_core_firmware_storage
- Testing: https://idm.yandex-team.ru/system/maps_core_firmware_storage_testing

## What happens when service is down
- It is not possible to manage firmwares and firmware rollouts.
- It is not possible to manage IDM roles in the system.
- IDM is unable to obtain role tree or manager roles in the system.


## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Fastcgi | /var/log/yandex/maps/firmware-storage/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : select * from hahn.`home/logfeller/logs/maps-log/1d/2018-02-28` where tskv_format='firmware-storage' |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Persistent Volumes
/logs - symlink from /var/log
