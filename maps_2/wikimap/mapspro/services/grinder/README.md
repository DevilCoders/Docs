# Core Nmaps Grinder

Инсталляция Grinder для Народной Карты: yacare-сервант grinder и демон grinder-master
## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Борис Чикунов (chikunov@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) <br> Илья Власюк (tail@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/grinder](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/grinder) |
| Сервис в ABC | [maps-core-nmaps-grinder](https://abc.yandex-team.ru/services/maps-core-nmaps-grinder/)|
| Проект в CI | [maps-core-nmaps-grinder](https://a.yandex-team.ru/projects/maps-core-nmaps-grinder/ci/actions/launches?dir=maps/wikimap/mapspro/services/grinder) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_grinder_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_stable/) | [ core-nmaps-grinder.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-stable-panel-main/) | [ maps_core_nmaps_grinder_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_grinder_stable) |
| Testing | [maps_core_nmaps_grinder_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_testing/) | [ core-nmaps-grinder.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-testing-panel-main/) | [ maps_core_nmaps_grinder_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_grinder_testing) |
| Unstable | [maps_core_nmaps_grinder_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_unstable/) | [ core-nmaps-grinder.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-unstable-panel-main/) | [ maps_core_nmaps_grinder_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_grinder_unstable) |


[Monitorings all (tag=a_prj_maps-core-nmaps-grinder)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-grinder)

| Staging | User panels |
| ------- | ----------- |
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-stable-panel-main |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-testing-panel-main |
| Unstable | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-grinder-unstable-panel-main |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-grinder.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-grinder.maps.yandex.net/) | [core-nmaps-grinder.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-grinder.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,msk;prj=core-nmaps-grinder-maps;signal=service_total) | [rtc_balancer_core-nmaps-grinder_maps_yandex_net_myt](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-grinder_maps_yandex_net_myt)<br>[rtc_balancer_core-nmaps-grinder_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-grinder_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-grinder_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-grinder_maps_yandex_net_vla) |
| Testing | Default | [core-nmaps-grinder.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-grinder.testing.maps.yandex.net/) | [core-nmaps-grinder.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-grinder.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-nmaps-grinder-testing-maps;signal=service_total) | [rtc_balancer_core-nmaps-grinder_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-grinder_testing_maps_yandex_net_sas) |
| Unstable | Default | [core-nmaps-grinder.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-grinder.unstable.maps.yandex.net/) | [core-nmaps-grinder.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-grinder.unstable.maps.yandex.net;itype=balancer;ctype=prod;locations=vla;prj=core-nmaps-grinder-unstable-maps;signal=service_total) | [rtc_balancer_core-nmaps-grinder_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-grinder_unstable_maps_yandex_net_vla) |


## What happens when service is down

Не будут запускаться длинные задачи из интерфейса Единой Карты (в том числе по расписанию).

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/grinder/* |
| Grinder master | /var/log/yandex/maps/wiki/grinder/* |
| wiki-tasks-invoker | /var/log/yandex/maps/wiki/tasks-invoker-worker/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-nmaps-grinder.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Сам гриндер ходит в:
- Mongo в MDB ([stable](https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-mongodb/cluster/mdbp3sjdks3836emnfnj), [testing+unstable](https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-mongodb/cluster/mdbfcm1rtpfrfuk6c22e))
- Менеджер задач НК для запуска задач по расписанию `http://core-nmaps.tasks.maps.yandex.net`

Проблемы в работе гриндера могут быть связаны в том числе с недоступностью или неполадками в этих сущностях.

## Documentation

[Устройство Grinder](https://wiki.yandex-team.ru/maps/dev/core/grinder/)

## Known clients
- maps-core-nmaps-tasks
- инстансы длинных задач, запущенных с помощью гриндера

## SLA

N/A


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_testing/yp_pods/ |
| Unstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_grinder_unstable/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_GRINDER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_GRINDER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_GRINDER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_GRINDER_TESTING_RTC_NETS_ ) |
| usntable | [ \_MAPS_CORE_NMAPS_GRINDER_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_GRINDER_UNSTABLE_RTC_NETS_ ) |

## Regression Stress Testing Configurations
N/A. Сервис малой нагрузки.
