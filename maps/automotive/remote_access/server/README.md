# Auto Remote Access Server
Сервер, принимающий запросы на удаленное управление автомобилем

## General information
| What | Who |
| ---- | --- |
| Дизайн-ревью| https://wiki.yandex-team.ru/Automotive/serverdevelopment/remote-acess-car-api/how-it-works/|
| Ответственные разработчики | Роман Пешкуро́в (peshkurov@yandex-team.ru) <br> Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Отвественные SRE | Роман Пешкуро́в (peshkurov@yandex-team.ru) <br> Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Исходники | [maps/automotive/remote_access/server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_access/server) |
| Сервис в ABC | [maps-auto-remote_access](https://abc.yandex-team.ru/services/maps-auto-remote_access/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_REMOTE_ACCESS |
| Sandbox builds - по желанию | https://sandbox.yandex-team.ru/task/574511330/view |
| Общая панель сервиса RemoteAccess | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_auto_remote_access/ |

Также над данными сервиса работает https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_access/pandora_poller/
Он обрабатывает данные сервиса в фоне.


## Service infrastructure

### Environments features

| Staging | Passport | Pandora | Cars |
| ------- | -------- | ------- | ---- |
| Stable | Prod | Real | User cars |
| Prestable | Prod | Real | Automotive carpark |
| Fakeprestable | Prod | Emulator | Fake cars |
| Testing | Test | Emulator | Fake cars |
| Stress | Stress | Emulator | Fake cars |

See also: [wiki page](https://wiki.yandex-team.ru/Automotive/serverdevelopment/remote-acess-car-api/how-it-works/#osobennostiokruzhenijj)


### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Fakeprestable | [maps_auto_remote_access_server_fakeprestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_access_server_fakeprestable/) | [ auto-remote-access-server.fakeprestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-access-server-fakeprestable-panel-main/) | [ maps_auto_remote_access_server_fakeprestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_access_server_fakeprestable) |
| Prestable | [maps_auto_remote_access_server_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_access_server_prestable/) | [ auto-remote-access-server.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-access-server-prestable-panel-main/) | [ maps_auto_remote_access_server_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_access_server_prestable) |
| Stable | [maps_auto_remote_access_server_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_access_server_stable/) | [ auto-remote-access-server.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-access-server-stable-panel-main/) | [ maps_auto_remote_access_server_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_access_server_stable) |
| Testing | [maps_auto_remote_access_server_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_access_server_testing/) | [ auto-remote-access-server.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-access-server-testing-panel-main/) | [ maps_auto_remote_access_server_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_access_server_testing) |
| Stress | [maps_auto_remote_access_server_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_access_server_stress/) | [ auto-remote-access-server.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-access-server-stress-panel-main/) | [ maps_auto_remote_access_server_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_access_server_stress) |

[Monitorings all (tag=a_prj_maps-auto-remote-access-server)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-remote-access-server)


### MDB Postgre clusters

| Staging | MDB cluster |
| ------- | ----------- |
| testing | [cluster](https://yc.yandex-team.ru/folders/foomvq199tj6fm1grcmk/managed-postgresql/cluster/mdbv8bl9e97dflucui9v) |
| stable | [cluster](https://yc.yandex-team.ru/folders/foomvq199tj6fm1grcmk/managed-postgresql/cluster/mdbrcdqsmg500cf0ho09) |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [auto-remote-access-server.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-remote-access-server.maps.yandex.net/) | [auto-remote-access-server.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-remote-access-server.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man;prj=auto-remote-access-server-maps;signal=service_total) | [rtc_balancer_auto-remote-access-server_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-access-server_maps_yandex_net_man)<br>[rtc_balancer_auto-remote-access-server_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-access-server_maps_yandex_net_sas) |
| Testing | Default | [auto-remote-access-server.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-remote-access-server.testing.maps.yandex.net/) | [auto-remote-access-server.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-remote-access-server.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man;prj=auto-remote-access-server-testing-maps;signal=service_total) | [rtc_balancer_auto-remote-access-server_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-access-server_testing_maps_yandex_net_man) |


## What happens when service is down

TODO: Накопить информацию. Но доподлинно известно, что у пользователей перестает работать удаленное управление автомобилем.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-remote-access-server/auto-remote-access-server.log |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ``SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-remote-access-server.maps.yandex.net' limit 1;`` |

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

## Regression Stress Testing Configurations
Шедулеры регрессионной стрельбы:

| imbalance + timings | https://sandbox.yandex-team.ru/scheduler/20443/view |
