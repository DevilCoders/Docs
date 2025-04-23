# Core Nmaps Social Activity (wiki-social-activity)

Активность пользователей НК.
Фид правок в тайле (фронт присылает limit=1).
Правки только от обычных пользователей (не роботы, не я.юзеры), не забаненные.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/social_activity](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/social_activity) |
| Сервис в ABC | [maps-core-nmaps-social-activity](https://abc.yandex-team.ru/services/maps-core-nmaps-social-activity/)|
| Проект в CI | [maps-core-nmaps-social-activity](https://a.yandex-team.ru/projects/maps-core-nmaps-social-activity/ci/actions/launches?dir=maps/wikimap/mapspro/services/social_activity) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_social_activity_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_stable/) | [ core-nmaps-social-activity.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-activity-stable-panel-main/) | [ maps_core_nmaps_social_activity_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_activity_stable) |
| Testing | [maps_core_nmaps_social_activity_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_testing/) | [ core-nmaps-social-activity.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-activity-testing-panel-main/) | [ maps_core_nmaps_social_activity_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_activity_testing) |
| Unstable | [maps_core_nmaps_social_activity_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_unstable/) | [ core-nmaps-social-activity.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-activity-unstable-panel-main/) | [ maps_core_nmaps_social_activity_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_activity_unstable) |


[Monitorings all (tag=a_prj_maps-core-nmaps-social-activity)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-social-activity)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-social-activity.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-social-activity.maps.yandex.net/) | [core-nmaps-social-activity.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-social-activity.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=core-nmaps-social-activity-maps;signal=service_total) | [rtc_balancer_core-nmaps-social-activity_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-activity_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-social-activity_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-activity_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-social-activity_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-activity_maps_yandex_net_vla) |

| Staging | URL |
| ------- | --- |
| Testing | core-nmaps-social-activity.common.testing.maps.yandex.net |
| Unstable | core-nmaps-social-activity.common.unstable.maps.yandex.net |


## What happens when service is down

База перегружена, сервис мониторит.
Пользователи, у которых включен монитор активности, не будут видеть пины с правками других пользователей.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/wiki-social-activity/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-11-21` WHERE vhost LIKE 'core-nmaps-social-activity.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients

https://puncher.yandex-team.ru/?destination=core-nmaps-social-activity.maps.yandex.net&rules=exclude_rejected&sort=destination&values=all

- Фронт НК


## SLA

Нет


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_stable/yp_pods |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_testing/yp_pods |
| Unstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_activity_unstable/yp_pods |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_TESTING_RTC_NETS_ ) |
| unstable | [ \_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_ACTIVITY_UNSTABLE_RTC_NETS_ ) |

