# Auto Lab Pandora Poller

Сервис осуществляет опрос сервиса [Pandora](https://pro.p-on.ru) для получения событий об изменениях состояний телематических блоков.
Сервис так же отправляет уведомления об изменениях состояния авто, отслеживает статус операций и синхронизирует настройки телематического блока.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики |  Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Роман Пешкуро́в (peshkurov@yandex-team.ru)  <br> Михаил Крутяков (mkrutyakov@yandex-team.ru)  |
| Отвественные SRE |  Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Роман Пешкуро́в (peshkurov@yandex-team.ru)  <br> Михаил Крутяков (mkrutyakov@yandex-team.ru)  |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_access/pandora_poller |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-auto-lab-pandora-poller/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_LAB_PANDORA_POLLER |
| Общая панель сервиса RemoteAccess | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_auto_remote_access/ |


Также над данными сервиса работает https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_access/server/
Он взаимдоействует с пользователями.

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Fakeprestable | [maps_auto_lab_pandora_poller_fakeprestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_poller_fakeprestable/) | [ auto-lab-pandora-poller.fakeprestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-poller-fakeprestable-panel-main/) | [ maps_auto_lab_pandora_poller_fakeprestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_poller_fakeprestable) |
| Prestable | [maps_auto_lab_pandora_poller_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_poller_prestable/) | [ auto-lab-pandora-poller.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-poller-prestable-panel-main/) | [ maps_auto_lab_pandora_poller_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_poller_prestable) |
| Stable | [maps_auto_lab_pandora_poller_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_poller_stable/) | [ auto-lab-pandora-poller.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-poller-stable-panel-main/) | [ maps_auto_lab_pandora_poller_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_poller_stable) |
| Testing | [maps_auto_lab_pandora_poller_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_poller_testing/) | [ auto-lab-pandora-poller.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-poller-testing-panel-main/) | [ maps_auto_lab_pandora_poller_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_poller_testing) |
| Stress | [maps_auto_lab_pandora_poller_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_poller_stress/) | [ auto-lab-pandora-poller.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-poller-stress-panel-main/) | [ maps_auto_lab_pandora_poller_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_poller_stress) |

[Monitorings all (tag=a_prj_maps-auto-lab-pandora-poller)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-lab-pandora-poller)


### MDB Postgre clusters

| Staging | MDB cluster |
| ------- | ----------- |
| testing | [cluster](https://yc.yandex-team.ru/folders/foomvq199tj6fm1grcmk/managed-postgresql/cluster/mdbv8bl9e97dflucui9v) |
| stable | [cluster](https://yc.yandex-team.ru/folders/foomvq199tj6fm1grcmk/managed-postgresql/cluster/mdbrcdqsmg500cf0ho09) |


## What happens when service is down

В случае проблем с сервисом могут наблюдаться проблемы:
 - с push уведомлениями
 - с промежуточными состояниями команд: lock/unlock, engine start, .... (будут завершаться по таймауту)
 - с синхронизацией настроек телематического блока
 - с завершением сценария продажи авто

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-remote-access-poller/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ``SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-pandora-poller.maps.yandex.ru' limit 1;`` |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
1. Сервис в своей работе активно использует API наших партнеров из pandora.
Иногда ребята отправляют свои сервера в даунтайм (отдают нам 500ки или не отвечают совсем), иногда меняют логику (отдают 400ки там, где их раньше не было) что приводит к 500м на нашей стороне и потере обновлений об автомобиле.
Для того, чтобы уметь отличать факапы с нашей стороны от их - есть два мониторинга:


### pandora-errors:

| Service | Juggler url |
| ------- | ----------- |
| server | [juggler](https://juggler.yandex-team.ru/check_details/?host=maps_auto_remote_access_server_stable&service=pandora-errors&last=1DAY) |
| poller | [juggler](https://juggler.yandex-team.ru/check_details/?host=maps_auto_lab_pandora_poller_stable&service=pandora-errors&last=1DAY) |

В случае, если горит какой-то из них - значит, что сервис пандоры отвечает неожиданным образом (5xx, 4xx на неожиданный запрос) для нас или не отвечает совсем. Это может очень по разному аффектить нас. Копим статистику кейсов.
Закешировать данные не получается - логичный флоу здесь - пятисотить.


## Documentation
https://wiki.yandex-team.ru/Automotive/serverdevelopment/remote-acess-car-api/

## Known clients
- Навигатор
- Будущая аппа Яндекс.Авто


## Гранты BlackBox
В [форме](https://grantushka.yandex-team.ru/grants/consumer/?namespace_id=11) искать maps-auto-remote_access_proxy

## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_REMOTE_ACCESS_SERVER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_ACCESS_SERVER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_REMOTE_ACCESS_SERVER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_ACCESS_SERVER_TESTING_RTC_NETS_ ) |
