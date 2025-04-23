# Core Factory Renderer

Сервис отвечает за рендеринг растровых и хотспотных тайлов в спутниковой фабрике:

- отображение границ и изображений снимков
- отображение рельефа

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE |  |
| Исходники | [maps/factory/services/renderer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/renderer) |
| Сервис в ABC | [maps-core-factory-renderer](https://abc.yandex-team.ru/services/maps-core-factory-renderer/)|
| CI (TestEnv) - Покоммитный | https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_FACTORY_RENDERER/history?limit=20 |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_renderer_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_renderer_stable/) | [ core-factory-renderer.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-renderer-stable-panel-main/) | [ maps_core_factory_renderer_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_renderer_stable) |
| Testing | [maps_core_factory_renderer_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_renderer_testing/) | [ core-factory-renderer.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-renderer-testing-panel-main/) | [ maps_core_factory_renderer_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_renderer_testing) |

[Monitorings all (tag=a_prj_maps-core-factory-renderer)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-renderer)

[Ratelimiter panel](https://yasm.yandex-team.ru/template/panel/maps_core_factory_renderer-ratelimiter2-panel)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-factory-renderer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-renderer.maps.yandex.net/) | [core-factory-renderer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-renderer.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-factory-renderer-maps;signal=service_total) | [rtc_balancer_core-factory-renderer_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-renderer_maps_yandex_net_man)<br>[rtc_balancer_core-factory-renderer_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-renderer_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-renderer_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-renderer_maps_yandex_net_vla) |
| Testing | Default | [core-factory-renderer.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-renderer.testing.maps.yandex.net/) | [core-factory-renderer.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-renderer.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla;prj=core-factory-renderer-testing-maps;signal=service_total) | [rtc_balancer_core-factory-renderer_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-renderer_testing_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-renderer_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-renderer_testing_maps_yandex_net_vla) |

## What happens when service is down

Не отображаются снимки на фабрике.

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/factory-renderer/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-factory-renderer.maps.yandex.net' limit 1; |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients

### Satellite factory

[Stable](https://factory-admin.maps.yandex-team.ru/)
[Testing](https://factory-admin.tst.c.maps.yandex-team.ru)

### Rdrproxy

https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/rdrproxy

## Persistent Volumes

* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
* /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_RENDERER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_RENDERER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_RENDERER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_RENDERER_TESTING_RTC_NETS_ ) |


