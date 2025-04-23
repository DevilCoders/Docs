# Core Feedback Userapi

API карточного фидбека для пользовательских запросов.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Анна Ждан (likynushka@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Анна Ждан (likynushka@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/feedback/userapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/userapi) |
| Сервис в ABC | [maps-core-feedback-userapi](https://abc.yandex-team.ru/services/maps-core-feedback-userapi/)|
| CI (TestEnv) - Покоммитный | [BUILD_DOCKER_MAPS_CORE_FEEDBACK_USERAPI](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_FEEDBACK_USERAPI) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_feedback_userapi_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_feedback_userapi_stable/) | [ core-feedback-userapi.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-feedback-userapi-stable-panel-main/) | [ maps_core_feedback_userapi_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_feedback_userapi_stable) |
| Testing | [maps_core_feedback_userapi_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_feedback_userapi_testing/) | [ core-feedback-userapi.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-feedback-userapi-testing-panel-main/) | [ maps_core_feedback_userapi_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_feedback_userapi_testing) |


[Monitorings all (tag=a_prj_maps-core-feedback-userapi)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-feedback-userapi)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-feedback-userapi.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-feedback-userapi.maps.yandex.net/) | [core-feedback-userapi.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-feedback-userapi.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=core-feedback-userapi-maps;signal=service_total) | [rtc_balancer_core-feedback-userapi_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-userapi_maps_yandex_net_man)<br>[rtc_balancer_core-feedback-userapi_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-userapi_maps_yandex_net_sas)<br>[rtc_balancer_core-feedback-userapi_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-userapi_maps_yandex_net_vla) |
| Testing | Default | [core-feedback-userapi.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-feedback-userapi.testing.maps.yandex.net/) | [core-feedback-userapi.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-feedback-userapi.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-feedback-userapi-testing-maps;signal=service_total) | [rtc_balancer_core-feedback-userapi_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-userapi_testing_maps_yandex_net_sas) |


## What happens when service is down

* Не обрабатываются пользовательские gdpr-запросы: не анонимизируются данные про фидбек на карте.
* Не отправляется фидбек на объекты на карте.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/feedback-userapi/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-feedback-userapi.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис



## Known clients
- Паспорт


## Как выкатить сервис
При выкатке нужно помнить про совместимость с [api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api). Для применения каких-то изменений может понадобиться выкатка обоих сервис
ов. Если нужно выкатить оба сервиса, то в каждом окружении сначала надо накатывать миграцию, а потом сервисы по очереди.

1. Выкатить миграцию в тестинг. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/migrations/README.md) по выкатке
2. Выкатить сервис в тестинг. [Документация sedem-а](https://docs.yandex-team.ru/sedem/releases)
5. Выкатить миграцию в прод. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
6. Выкатить сервис в прод

## Documentation

[Документация](https://docs.yandex-team.ru/maps-feedback/)

На текущий момент обрабатываются следующие запросы:
* gdpr-запросы. [Спецификация](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/).
* Ручки создания фидбэка: `POST /v1/tasks` и `POST /v1/tasks/batch`. [Документация](https://docs.yandex-team.ru/maps-feedback/service/api), [примеры запросов](https://docs.yandex-team.ru/maps-feedback/service/examples).

Для всех запросов для авторизации нужен tvm Service-тикет и User-тикет.
   - tvm-id в тестинге: `2026526`
   - tvm-id в проде: `2026524`

В ручках создания фидбэка запросы для авторизованных пользователей дополнительно принимают tvm User-тикет. В таком случае в теле запроса `uid` и `user_email` должны отсутствовать. Эти данные будут получены из [ручки blackbox](https://docs.yandex-team.ru/blackbox/methods/user_ticket) по User-тикету.

## SLA

Нет.


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FEEDBACK_USERAPI_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FEEDBACK_USERAPI_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FEEDBACK_USERAPI_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FEEDBACK_USERAPI_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

Нет.

