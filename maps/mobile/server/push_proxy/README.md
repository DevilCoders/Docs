# Core Push Proxy

Сервис отвечает за передачу push-токена, полученного устройством, в систему отправки пуш-уведмлений [Xiva](https://console.push.yandex-team.ru).
Push-токен - это токен, получаемый при запуске приложения (а также логине и подобных событиях) устройством от платформенного сервиса пушей (APNs или GCM/FCM).
После того, как устройство (push-токен) зарегистрировано в Xiva, сообщения доставляются пользвателю без участия сервиса push-proxy.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Пётр Гриневич (grinev@yandex-team.ru), Александр Любицкий (innocent@yandex-team.ru) |
| Отвественные SRE | Пётр Гриневич (grinev@yandex-team.ru), Александр Любицкий (innocent@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/push_proxy |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-push-proxy/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_PUSH_PROXY |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_push_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_push_proxy_stable/) | [ core-push-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-push-proxy-stable-panel-main/) | [ maps_core_push_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_push_proxy_stable) |
| Prestable | [maps_core_push_proxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_push_proxy_prestable/) | [ core-push-proxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-push-proxy-prestable-panel-main/) | [ maps_core_push_proxy_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_push_proxy_prestable) |
| Testing | [maps_core_push_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_push_proxy_testing/) | [ core-push-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-push-proxy-testing-panel-main/) | [ maps_core_push_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_push_proxy_testing) |
[Monitorings all (tag=a_prj_maps-core-push-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-push-proxy)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-push-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-push-proxy.maps.yandex.net/) | [core-push-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-push-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-push-proxy-maps;signal=service_total) | [rtc_balancer_core-push-proxy_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-push-proxy_maps_yandex_net_man)<br>[rtc_balancer_core-push-proxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-push-proxy_maps_yandex_net_sas)<br>[rtc_balancer_core-push-proxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-push-proxy_maps_yandex_net_vla) |
| Testing | Default | [core-push-proxy.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-push-proxy.testing.maps.yandex.net/) | [core-push-proxy.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-push-proxy.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-push-proxy-testing-maps;signal=service_total) | [rtc_balancer_core-push-proxy_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-push-proxy_testing_maps_yandex_net_sas) |
## What happens when service is down

Устройства пользователей не смогут зарегистрировать или обновить push-токен в Xiva и, соответственно, пользователи, у которых push-токен протух, перестанут получать пуш-уведомления. Тем пользователям, у которых push-токен жив, уведомления продолжат приходить.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/push-proxy/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2019-12-02\` WHERE vhost LIKE 'core-push-proxy.maps.yandex.net' limit 1; |

## How to fix common problems
Первым делом надо проверить, всё ли хорошо у самой Xiva: <br>
[Общая панель Xiva](https://yasm.yandex-team.ru/template/panel/xiva_main_panel/env=production/?range=21600000) <br>
[Тайминги  subscribe_app](https://yasm.yandex-team.ru/chart/signals=%7Bquant(push-http_timings_v2_subscribe_app_hhhh,99),quant(push-http_timings_v2_subscribe_app_hhhh,95),quant(push-http_timings_v2_subscribe_app_hhhh,90),quant(push-http_timings_v2_subscribe_app_hhhh,75),quant(push-http_timings_v2_subscribe_app_hhhh,50)%7D;hosts=CON;itype=push;ctype=production;prj=xiva-server/?range=21600000) <br>
Если невооруженным глазом видна аномалия в таймингах - имеет смысл написать на
xiva-dev@ <br>
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

[Общее описание сервиса (некоторые детали устарели)](https://wiki.yandex-team.ru/aleksandrljubickijj/push/)

[Ручки на Мобильной Проксе](https://wiki.yandex-team.ru/maps/dev/core/mobile/services/push/)

## Known clients
 - maps_core_mobile_proxy

## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_mobile_proxy_push) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_mobile_proxy_push.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_PUSH_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PUSH_PROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_PUSH_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PUSH_PROXY_TESTING_RTC_NETS_ ) |

## TVM Auth
Сервис имеет зарегистрированные TVM-приложения, однако от  собственно TVM используется только получение uid по User-тикетам

## Regression
Регулярное регрессионное тестировнние не настраивалось по причинам
  - низкого RPS
  - необходимости иметь постоянные выделенные ресурсы как для мишени, так и для заглушки (сервиса, имеющего интерфейс Xiva и эмулирующего тайминги настоящей Xivа), в которую push-proxy будет ходить.

Рекомендуется раз в год запускать стрельбы руками