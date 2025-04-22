# Auto Lab Pandora Emulator

Emulates Pandora car alarm server API for testing purposes.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Крутяков (mkrutyakov@yandex-team.ru)<br> Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Отвественные SRE | Роман Пешкуро́в (peshkurov@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_access/pandora_emulator |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-auto-lab-pandora-emulator/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_LAB_PANDORA_EMULATOR |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Testing | [maps_auto_lab_pandora_emulator_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_emulator_testing/) | [ auto-lab-pandora-emulator.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-lab-pandora-emulator-testing-panel-main/) | [ maps_auto_lab_pandora_emulator_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_lab_pandora_emulator_testing) |
[Monitorings all (tag=a_prj_maps-auto-lab-pandora-emulator)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-lab-pandora-emulator)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Testing | Default | [auto-remote-access-server.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-remote-access-server.testing.maps.yandex.net/) | [auto-remote-access-server.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-remote-access-server.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man;prj=auto-remote-access-server-testing-maps;signal=service_total) | [rtc_balancer_auto-remote-access-server_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-access-server_testing_maps_yandex_net_man/)


## What happens when service is down

Auto Lab Remote Access Server/Poller testing and fakeprestable stagings won't operate correctly.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-lab-pandora-emulator/auto-lab-pandora-emulator.log |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Need collect cases

## Documentation

[Информация по вспомогательным ручкам](https://wiki.yandex-team.ru/Automotive/serverdevelopment/remote-acess-car-api/util/)

## Known clients
- Auto Lab Remote Access Server (testing)
- Auto Lab Remote Access Server (fakeprestable)
- Auto Lab Remote Access Poller (testing)
- Auto Lab Remote Access Poller (fakeprestable)

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_lab_pandora_emulator_testing/yp_pods/ |

## Golovan panels

TODO: Добавить панели в Головане и прописать их тут

## Firewall macroses
| staging | URL |
|---|---|
| testing | [ \_MAPS_AUTO_REMOTE_ACCESS_SERVER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_ACCESS_SERVER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
