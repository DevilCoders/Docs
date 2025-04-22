# Core Pht Proxy

Maps photos public proxy for avatars images. Allow to upload and download photos.

Personal photos request must have passport cookie authorization. Public photos are available without an autorization.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Отвественные SRE | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Исходники | [maps/photos/proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/photos/proxy) |
| Сервис в ABC | [maps-core-pht-proxy](https://abc.yandex-team.ru/services/maps-core-pht-proxy/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_PHT_PROXY |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_pht_proxy_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_load/) | [ core-pht-proxy.load ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-proxy-load-panel-main/) | [ maps_core_pht_proxy_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_proxy_load) |
| Prestable | [maps_core_pht_proxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_prestable/) | [ core-pht-proxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-proxy-prestable-panel-main/) | [ maps_core_pht_proxy_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_proxy_prestable) |
| Stable | [maps_core_pht_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_stable/) | [ core-pht-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-proxy-stable-panel-main/) | [ maps_core_pht_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_proxy_stable) |
| Testing | [maps_core_pht_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_testing/) | [ core-pht-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-proxy-testing-panel-main/) | [ maps_core_pht_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_proxy_testing) |


[Monitorings all (tag=a_prj_maps-core-pht-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-pht-proxy)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-pht-proxy.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-pht-proxy.maps.yandex.ru/) | [core-pht-proxy.maps.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-pht-proxy.maps.yandex.ru;itype=balancer;ctype=prod;locations=vla,man,sas;prj=core-pht-proxy-maps;signal=service_total) | [rtc_balancer_core-pht-proxy_maps_yandex_ru_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-proxy_maps_yandex_ru_man)<br>[rtc_balancer_core-pht-proxy_maps_yandex_ru_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-proxy_maps_yandex_ru_sas)<br>[rtc_balancer_core-pht-proxy_maps_yandex_ru_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-proxy_maps_yandex_ru_vla) |


## What happens when service is down

Не показываются фотографии фотослоя на яндекс картах. Не кликаются фотографии при поиске топонимов. Нельзя загрузить новые фотографии в личном кабинете.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-pht-proxy.maps.yandex.ru' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc) <br>

Это просто nginx прокси торчащая наружу с проверкой авторизационных <br>
Первое что надо сделать проверить что все ок с core-pht-ugc.maps.yandex.net https://a.yandex-team.ru/arc/trunk/arcadia/maps/photos/ugc/readme.md 

## Documentation

Ручки прокси https://a.yandex-team.ru/arc/trunk/arcadia/maps/photos/proxy/api.md <br>
Компонтенты системы https://wiki.yandex-team.ru/jandekskarty/projects/catalog/ek/ek-nk/projects/disk-maps-photo/mapsphotolayer/ <br>
Протоколы https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/photougc <br>
Примеры использования https://wiki.yandex-team.ru/user/idg/maps_photolayer_helpfull_info/ <br>

## Known clients
Яндекс Карты. Личный кабинет Яндекс Карт.


## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_pht_proxy) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_pht_proxy.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_testing/yp_pods |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_prestable/ |
| Production | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_stable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_proxy_load/ |



## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_PHT_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_PROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_PHT_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_PROXY_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSPANO
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/43920
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/43918
    * Тикет: https://st.yandex-team.ru/MAPSPANO-648

