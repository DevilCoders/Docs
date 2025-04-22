# Core Nmaps Social Backoffice (wiki-social-backoffice)

Сервис обработки запросов от фоновых процессов, таких как генераторы гипотез.
В этот сервис не должны прилетать пользовательские запросы от фронтенда НК.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/social_backoffice](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/social_backoffice) |
| Сервис в ABC | [maps-core-nmaps-social-backoffice](https://abc.yandex-team.ru/services/maps-core-nmaps-social-backoffice/)|
| Проект в CI | [maps-core-nmaps-social-backoffice](https://a.yandex-team.ru/projects/maps-core-nmaps-social-backoffice/ci/actions/launches?dir=maps/wikimap/mapspro/services/social_backoffice) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_social_backoffice_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_backoffice_stable/) | [ core-nmaps-social-backoffice.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-backoffice-stable-panel-main/) | [ maps_core_nmaps_social_backoffice_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_backoffice_stable) |
| Testing | [maps_core_nmaps_social_backoffice_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_backoffice_testing/) | [ core-nmaps-social-backoffice.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-backoffice-testing-panel-main/) | [ maps_core_nmaps_social_backoffice_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_backoffice_testing) |
| Unstable | [maps_core_nmaps_social_backoffice_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_backoffice_unstable/) | [ core-nmaps-social-backoffice.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-backoffice-unstable-panel-main/) | [ maps_core_nmaps_social_backoffice_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_social_backoffice_unstable) |


[Monitorings all (tag=a_prj_maps-core-nmaps-social-backoffice)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-social-backoffice)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-social-backoffice.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-social-backoffice.maps.yandex.net/) | [core-nmaps-social-backoffice.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-social-backoffice.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=core-nmaps-social-backoffice-maps;signal=service_total) | [rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social-backoffice_maps_yandex_net_vla) |

### Balancers URLs
- Stable: http://core-nmaps-social-backoffice.maps.yandex.net
- Testing: http://core-nmaps-social-backoffice.common.testing.maps.yandex.net
- Unstable: http://core-nmaps-social-backoffice.common.unstable.maps.yandex.net


## What happens when service is down

Клиенты не смогут создавать гипотезы.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/wiki-social-backoffice/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-nmaps-social-backoffice.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Будут проблемы - будем решать! ;) (с)Решала

## Documentation

Схема: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/social

## Known clients
- [АРМ экспертов Яндекс.Пробок](https://abc.yandex-team.ru/services/maps-core-jams-arm)
- [Генератор гипотез о перекрытиях по realtime GPS сигналам](https://abc.yandex-team.ru/services/maps-core-gpsrealtime-hypgen)
- [Генератор гипотез по инфоточкам](https://abc.yandex-team.ru/services/maps-core-infopoints-hypgen)
- [NMAPS Генератор гипотез об ошибках карты](https://abc.yandex-team.ru/services/maps-core-nmaps-hypgen)
- [MRC воркер пешеходного сценария](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-onfoot-processor)
- [MRC длинные задачи](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-lt)
- [MRC генератор гипотез об ошибках в карте](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-signsdetector)
- [Обработка фидбэка в Народной Карте](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-feedback)
- [Интеграция Народной Карты и Справочника](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-sprav)
- [Компоненты связности дорожного графа](https://abc.yandex-team.ru/services/maps-core-conn-checker)
- [Отгрузка POI в НК для повышения качества координат](https://abc.yandex-team.ru/services/maps-core-static-poi-2-nmaps)
- [Метрики навигации](https://abc.yandex-team.ru/services/maps-core-navi-statistics)


## Ratelimiter

[stable/testing](https://yasm.yandex-team.ru/template/panel/maps_core_nmaps_social_backoffice-ratelimiter2-panel)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_TESTING_RTC_NETS_ ) |
| unstable | [ \_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_SOCIAL_BACKOFFICE_UNSTABLE_RTC_NETS_ ) |
