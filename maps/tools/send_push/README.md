# Core Send Push
Стенд для тестовой отправки пуш-уведомлений в yandex-maps-pushapp

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Любицкий (innocent@yandex-team.ru) Пётр Гриневич (grinev@yandex-team.ru) |
| Отвественные SRE | Александр Любицкий (innocent@yandex-team.ru) Пётр Гриневич (grinev@yandex-team.ru) |
| Исходники | [maps/tools/send_push](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/send_push) |
| Сервис в ABC | [maps-core-send-push](https://abc.yandex-team.ru/services/maps-core-send-push/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_SEND_PUSH |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_send_push_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_send_push_stable/) | [ core-send-push.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-send-push-stable-panel-main/) | [ maps_core_send_push_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_send_push_stable) |

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-send-push.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-send-push.maps.yandex.net/) | [core-send-push.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-send-push.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla;prj=core-send-push-maps;signal=service_total) | [rtc_balancer_core-send-push_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-send-push_maps_yandex_net_sas)<br>[rtc_balancer_core-send-push_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-send-push_maps_yandex_net_vla) |


## What happens when service is down

Нельзя будет отправить тестовое пуш-уведомление

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_SEND_PUSH_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SEND_PUSH_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_SEND_PUSH_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SEND_PUSH_TESTING_RTC_NETS_ ) |
