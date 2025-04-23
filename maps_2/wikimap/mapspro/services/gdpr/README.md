# Core Nmaps Gdpr

GDPR сервис Народной Карты.
Обслуживает запросы из Паспорта для удаление/анонимизации пользовательской информации.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/gdpr](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/gdpr) |
| Сервис в ABC | [maps-core-nmaps-gdpr](https://abc.yandex-team.ru/services/maps-core-nmaps-gdpr/)|
| Проект в CI | [maps-core-nmaps-gdpr](https://a.yandex-team.ru/projects/maps-core-nmaps-gdpr/ci/actions/launches?dir=maps/wikimap/mapspro/services/gdpr) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_gdpr_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_gdpr_stable/) | [ core-nmaps-gdpr.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-gdpr-stable-panel-main/) | [ maps_core_nmaps_gdpr_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_gdpr_stable) |
| Testing | [maps_core_nmaps_gdpr_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_gdpr_testing/) | [ core-nmaps-gdpr.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-gdpr-testing-panel-main/) | [ maps_core_nmaps_gdpr_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_gdpr_testing) |


[Monitorings all (tag=a_prj_maps-core-nmaps-gdpr)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-gdpr)

| Staging | User panels |
| ------- | ----------- |
| Stable | [maps_core_nmaps_gdpr_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_gdpr_stable) |
| Testing | [maps_core_nmaps_gdpr_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_gdpr_testing) |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-gdpr.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-gdpr.maps.yandex.net/) | [core-nmaps-gdpr.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-gdpr.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-nmaps-gdpr-maps;signal=service_total) | [rtc_balancer_core-nmaps-gdpr_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-gdpr_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-gdpr_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-gdpr_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-gdpr_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-gdpr_maps_yandex_net_vla) |


## What happens when service is down

Сервис не будет принимать запросы о ходе и инициации удаления пользовательской информации.


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/wiki-gdpr/* |
| wiki-gdpr-worker | /var/log/yandex/maps/wiki-gdpr-worker/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-nmaps-gdpr.maps.yandex.net' limit 1; |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис
1) Протереть лобовое стекло чистой тряпкой
2) Выйти из машины, попинать колесо и зайти заново
3) "Будут проблемы - будем решать!" (с)Решала ;)


## Documentation

[Требования к API](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/)
[GDPR в НК](https://wiki.yandex-team.ru/alekseyponomarev/gdpr/)

Yacare-сервис принимает gdpr-заявки на анонимизацию/удаление пользовательских данных в Народной Карте (НК).
* /takeout/status/ - возвращает статус пользовательских данных (в процессе удаления, есть что удалить, пусто)
* /takeout/delete/ - создает заявку в core-базе НК, процесс анонимизации/удаления выполняется вручную.

В докере /usr/bin/wiki-gdpr-tool, который умеет создавать gdpr-заявки вручную, анонимизировать/удалять пользовательские данные.


Параметры запуска:
| Опция | Обязательный | Описание |
| ----- | ------------ | -------- |
| --config <filename> | Нет | Путь до services.xml |
| --uid <n> | Да | Паспортный UID пользователя |
| --action <value> | Да | Атомарное действие |
| --request-id <value> | Нет | Используется только в action=start |
| --dry-run | Нет | Не сохраняем результаты в базе |

Action:
* start - старт gdpr-заявки, аналог http-ручки /takeout/delete/ (status -> delete_in_progress)
* status - проверка статуса - используется общий код с http /takeout/status/
* info - расширенная информация - список всех gdpr-заявок
* anonymize-edits - анонимизация правок и подписок
* anonymize-comments - анонимизация комментариев
* anonymize-feedback - анонимизация задач фидбэка в НК
* anonymize-moderation - анонимизация задач модерации НК (автор принятия и закрытия задачи)
* anonymize-sprav - анонимизация фидбэка в Справочник из НК
* clean-acl-profile - очистка acl-профиля (если пользователь забанен, то оставляет последний бан), бэкапит и оставляет только acl-группы nmaps и nmaps-novice
* clean-social-profile - очистка социального профиля, бэкапит и удаляет все данных из таблиц профиля, бэджей, авто-скилов, настроек пользователя для браузера
* clean-stats - очистка статистики, бэкапит и удаляет данные из таблиц статистики, рейтинг обнулится автоматически
* finish - финализация процесса, gdpr-заявка считается выполненной, фиксируется время окончания, status -> empty если выполнены все перечисленные выше пункты по анонимизации


Код, содержащий знания о схеме данных или "хакерские" запросы по удалению и анонимизации данных (не вошедший в состав публичного API wiki-библиотек), см. [библиотеку](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/gdpr/src/lib):
| Файл | Описание |
| ---- | -------- |
| [sql_string.h](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/gdpr/src/lib/sql_string.h) | названия схем, таблиц, колонок |
| [utils.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/gdpr/src/lib/utils.cpp) | функции, необходимые для HTTP-сервиса информировании о статусе процесса удаления |
| [worker.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/gdpr/src/lib/worker.cpp) | функции, необходимые для работы утилиты wiki-gdpr-tool - зачистка пользовательской информации |


Cron-джоба занимается автоматическим отложенным выполнением gdpr-заявок. Процесс выбирает заявки, созданные 7 и более суток назад и берёт их в обработку. Предполагается, что за это время анонимизируемые правки успеют пройти штатную модерацию в неанонимизированном виде.


## Known clients

[Puncher](https://puncher.yandex-team.ru/?destination=core-nmaps-gdpr.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination)

* Я.Паспорт


## SLA

Нет


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | [maps_core_nmaps_gdpr_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_gdpr_stable/yp_pods/) |
| Testing | [maps_core_nmaps_gdpr_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_gdpr_testing/yp_pods/) |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_GDPR_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_GDPR_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_GDPR_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_GDPR_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

Нет

