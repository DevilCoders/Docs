# Core Pht Ugc

Maps photos API. Allows to upload photos and get/update photos metadata.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Отвественные SRE | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Исходники | [maps/photos/ugc](https://a.yandex-team.ru/arc/trunk/arcadia/maps/photos/ugc) |
| Сервис в ABC | [maps-core-pht-ugc](https://abc.yandex-team.ru/services/maps-core-pht-ugc/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_PHT_UGC |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_pht_ugc_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_load/) | [ core-pht-ugc.load ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-ugc-load-panel-main/) | [ maps_core_pht_ugc_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_ugc_load) |
| Prestable | [maps_core_pht_ugc_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_prestable/) | [ core-pht-ugc.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-ugc-prestable-panel-main/) | [ maps_core_pht_ugc_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_ugc_prestable) |
| Stable | [maps_core_pht_ugc_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_stable/) | [ core-pht-ugc.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-ugc-stable-panel-main/) | [ maps_core_pht_ugc_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_ugc_stable) |
| Testing | [maps_core_pht_ugc_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_testing/) | [ core-pht-ugc.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-ugc-testing-panel-main/) | [ maps_core_pht_ugc_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_ugc_testing) |


[Monitorings all (tag=a_prj_maps-core-pht-ugc)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-pht-ugc)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-pht-ugc.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-pht-ugc.maps.yandex.net/) | [core-pht-ugc.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-pht-ugc.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-pht-ugc-maps;signal=service_total) | [rtc_balancer_core-pht-ugc_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-ugc_maps_yandex_net_man)<br>[rtc_balancer_core-pht-ugc_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-ugc_maps_yandex_net_sas)<br>[rtc_balancer_core-pht-ugc_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-ugc_maps_yandex_net_vla) |


## What happens when service is down

Пользователи не могут кликать и просмативать фотографии на карте. В личном кабинете нельзя загрузить новое фото.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/pht_ugc/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-pht-ugc.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc) <br>
Проверить все ли ок с базой данных <br>
https://yc.yandex-team.ru/folders/foo9er4u58k7oplgfj1q/managed-postgresql/cluster/mdbnkbtpa19nd4j9dp4e?section=monitoring <br>
Посмотреть логи все ли впорядке с аватарницей <br>

## Documentation

Компонтенты системы https://wiki.yandex-team.ru/jandekskarty/projects/catalog/ek/ek-nk/projects/disk-maps-photo/mapsphotolayer/ <br>
Протоколы https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/photougc <br>
Примеры использования https://wiki.yandex-team.ru/user/idg/maps_photolayer_helpfull_info/ <br>

## Known clients
Яндекс Карты. Личный кабинет Яндекс Карт. <br>


## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_pht_ugc) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_pht_ugc.py)

## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_testing/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_prestable/ |
| Production | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_stable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_ugc_load/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_PHT_UGC_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_UGC_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_PHT_UGC_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_UGC_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSPANO
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/43629
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/43628
    * Тикет: https://st.yandex-team.ru/MAPSPANO-648
