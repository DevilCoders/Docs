# Core Nmaps Mrc Ugc Back

Бекенд раздела Зеркал для Личного кабинета пользователя.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Андрей Наплавков (naplavkov@yandex-team.ru) <br> Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Андрей Наплавков (naplavkov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/mrc/ugc_back](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/ugc_back) |
| Сервис в ABC | [maps-core-nmaps-mrc-ugc-back](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-ugc-back/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_UGC_BACK |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_ugc_back_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_ugc_back_stable/) | [ core-nmaps-mrc-ugc-back.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-ugc-back-stable-panel-main/) | [ maps_core_nmaps_mrc_ugc_back_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_ugc_back_stable) |
| Testing | [maps_core_nmaps_mrc_ugc_back_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_ugc_back_testing/) | [ core-nmaps-mrc-ugc-back.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-ugc-back-testing-panel-main/) | [ maps_core_nmaps_mrc_ugc_back_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_ugc_back_testing) |


[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-ugc-back)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-ugc-back)
[Ratelimiter panel](https://yasm.yandex-team.ru/template/panel/maps_core_nmaps_mrc_ugc_back-ratelimiter2-panel)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-mrc-ugc-back.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-ugc-back.maps.yandex.net/) | [core-nmaps-mrc-ugc-back.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-mrc-ugc-back.maps.yandex.net;itype=balancer;ctype=prod;locations=;prj=core-nmaps-mrc-ugc-back-maps;signal=service_total) | [rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-ugc-back_maps_yandex_net_vla) |
| Testing | Default | [core-nmaps-mrc-ugc-back.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-nmaps-mrc-ugc-back.common.testing.maps.yandex.net_default/show/) |  |  |


## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/mrc-ugc-back/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-01-20` WHERE vhost LIKE ''mrc-ugc-back'.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients
- TODO: Сюда напишите список известных клиентов
- ????




## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_MRC_UGC_BACK_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_UGC_BACK_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_MRC_UGC_BACK_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_UGC_BACK_TESTING_RTC_NETS_ ) |


