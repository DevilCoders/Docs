# Core Ugc Account

[**Фронтофис Maps UGC Account**](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Api.md) - часть [**Maps UGC Account**](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md), в которую приходят пользовательские запросы из ui.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Анна Ждан (likynushka@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) |
| Отвественные SRE | Анна Ждан (likynushka@yandex-team.ru)  <br> Алексей Пономарев (ponomarev@yandex-team.ru)  <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/ugc/account](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/account) |
| Сервис в ABC | [maps-core-ugc-account](https://abc.yandex-team.ru/services/maps-core-ugc-account/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_UGC_ACCOUNT |


## Service infrastructure

### Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` and `X-Ya-User-Ticket` HTTP headers. [About user tickets](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/).

Environment  | TVM Application ID
-------------|-------------------
testing      | [2025128](https://abc.yandex-team.ru/services/maps-core-ugc-account/resources/)
production   | [2025126](https://abc.yandex-team.ru/services/maps-core-ugc-account/resources/)

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_ugc_account_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_stable/) | [ core-ugc-account.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-ugc-account-stable-panel-main/) | [ maps_core_ugc_account_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ugc_account_stable) |
| Prestable | [maps_core_ugc_account_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_prestable/) | [ core-ugc-account.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-ugc-account-prestable-panel-main/) | [ maps_core_ugc_account_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ugc_account_prestable) |
| Testing | [maps_core_ugc_account_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_testing/) | [ core-ugc-account.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-ugc-account-testing-panel-main/) | [ maps_core_ugc_account_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ugc_account_testing) |


[Monitorings all (tag=a_prj_maps-core-ugc-account)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-ugc-account)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-ugc-account.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ugc-account.maps.yandex.net/) | [core-ugc-account.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ugc-account.maps.yandex.net;itype=balancer;ctype=prod;locations=;prj=core-ugc-account-maps;signal=service_total) |  |
| Testing | Default | [core-ugc-account.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ugc-account.testing.maps.yandex.net/) | [core-ugc-account.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ugc-account.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=;prj=core-ugc-account-testing-maps;signal=service_total) |  |


## What happens when service is down

Не отображаются/тормозят вкладки "Исправления", "Задачи", "Фото", "Зеркала" в личном кабинете карт

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-ugc-account.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Как выкатить сервис

При выкатке нужно помнить про совместимость с [backoffice](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/backoffice). В некоторых ситуациях может быть важен порядок выкатки этих сервисов. При правках [https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/](протобуфов) или общих библиотек выкатывать нужно оба сервиса.

1. Выкатить миграцию в тестинг. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
2. Выкатить сервис в тестинг. [Документация sedem-а](https://docs.yandex-team.ru/sedem/releases)
3. Проверить, что личный кабинет работает: https://l7test.yandex.ru/maps/profile/ugc/feedback
4. Убедиться, что работают [стрельбы](https://lunapark.yandex-team.ru/regress/NMAPS?service=UGC account). [Документация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/prepare_ammo/Readme.md) по стрельбам
5. Выкатить миграцию в прод. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
6. Выкатить сервис в прод
7. Убедиться, что личный кабинет работает: https://maps.yandex.ru/profile/ugc/feedback

## Documentation

Форматы и документация [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md).

## Known clients
- https://abc.yandex-team.ru/services/maps-front-maps

Все клиенты отражены в [конфиге ratelimiter-а](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_ugc_account/)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_account_testing/yp_pods/ |

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_UGC_ACCOUNT_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_UGC_ACCOUNT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_UGC_ACCOUNT_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_UGC_ACCOUNT_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Lunapark: https://lunapark.yandex-team.ru/regress/NMAPS?service=UGC%20account
* Lunapark: https://lunapark.yandex-team.ru/NMAPS-13013
* Тикет: https://st.yandex-team.ru/NMAPS-13013
* Документация про стрельбы [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/prepare_backoffice_ammo/Readme.md)

#### Планировщики стрельб в sandbox:
* Получение ленты contribution-ов на разладку: https://sandbox.yandex-team.ru/scheduler/44612
* Получение ленты contribution-ов с постоянной нагрузкой: https://sandbox.yandex-team.ru/scheduler/44617
* Получение ленты assignment-ов на разладку: https://sandbox.yandex-team.ru/scheduler/44610
* Получение ленты assignment-ов с постоянной нагрузкой: https://sandbox.yandex-team.ru/scheduler/44616

## Репликация на YT
Настроена репликация из базы UGC PostgreSQL на YT. Реплицируемые таблицы:
```
ugc.assignment
```
Директория YT: [hahn.//home/maps/core/nmaps/dynamic/replica/ugc](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/ugc)

#### Устройство репликации
Реликация производится с помощью Data Transfer в Yandex Cloud.
В связи с тем, что база шардирована, потребовались следующие артефакты:
* [9 эндпоинтов](https://yc.yandex-team.ru/folders/akubui5hvdelt2hni2a3/data-transfer): 8 PostgreSQL и 1 YT;
* [8 трансферов]((https://yc.yandex-team.ru/folders/akubui5hvdelt2hni2a3/data-transfer/transfers)): каждый -- между одним эндпоинтом PostgreSQL и папкой в YT.

#### Способ рестарта
В связи с таким устройством, рестарт репликации в случае необходимости (при downtime Hahn; добавлении таблиц; ошибок репликации, отображаемых в статусе трансферов) происходит в несколько этапов:

1. Остановить транферы (убедиться, что остановлены все).
1. Удалить YT-таблицы в папке назначения (например, `ugc_assignment`).
1. Активировать трансферы.

Таблицы необходимо удалять вручную, т. к. хотя для эндпоинтов DT существуют политики очистки `DROP` и `TRUNCATE`, они учитываются при каждом рестарте каждого из трансферов. Их применение означало бы невозможность корректного рестарта набора трансферов с общим приемником.

#### Мониторинг репликации

Juggler aggregate: [check_details/?host=solomon-alert&service=nmaps_dynamic_replica_ugc](https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_ugc).

Solomon alert: [maps-nmaps/alerts/2d540764-acfd-4e11-972e-5eb26e746254](https://solomon.yandex-team.ru/admin/projects/maps-nmaps/alerts/2d540764-acfd-4e11-972e-5eb26e746254).

Общий график задержки репликации восьми трафнсферов: [кастомный](https://monitoring.yandex-team.ru/projects/data-transfer/explorer/queries?q.0.text=%7Bproject%3D%22data-transfer%22%2C%20cluster%3D%22rtc-prod%22%2C%20service%3D%22data-plane%22%2C%20resource_type%3D%22transfer%22%2C%20resource_id%3D%22dttoj72gtj99f16g1gn9%7Cdtt0jo3sp0bup0o87ns2%7Cdttonitmrrff6fh89cnv%7Cdtteoilnqm2jstvva6qs%7Cdttvk8ioh398c6bl2dea%7Cdttldeld35s8rda87n1c%7Cdttq3rrd3t66vcr5fi5n%7Cdttpk259kcflk3ibfemq%22%2C%20name%3D%22sinker.pusher.time.row_max_lag_sec%22%2C%20operation_type%3D%22-%22%7D&refresh=60&range=1d&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default).

Для каждого из [трансферов](https://yc.yandex-team.ru/folders/akubui5hvdelt2hni2a3/data-transfer/transfers) в его настройках в YC есть "Cсылка на дашборд" с графиками.
