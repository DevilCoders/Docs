# Core Time
Сервер позволяет мапкиту узнать настоящее время для случаев, когда в клиенте выставлено неправильное время или неверный часовой пояс.

Часовые пояса время от времени меняются (см.[изменения в России](https://ru.wikipedia.org/wiki/Время_в_России#Состоявшиеся_изменения) ). Производители телефонов при этом выпускают обновления для новых устройств, а у более старых устройств может остаться старая информация о часовых поясах. Пользователи же не пытаются разобраться, почему телефон показывает неправильное время, а корректируют часы так, чтобы время выглядело нормально. Системное время в UTC при этом получается сдвинутым (обычно на час). Из-за этого в тех местах, где время о событии получается с сервера в UTC, а отображать нужно, сколько осталось до этого события, может показываться значение со сдвигом. Например, если пользователь сдвинул время на час назад, то в прогнозе прибытия автобуса у него может отображаться не "через 1 мин", а "через 61 мин".
Сервис Core Time позволяет получить из мапкита настоящее серверное время (компонента [AdjustedClock](https://git.yandex-team.ru/gitweb/maps/mapsmobi.git?a=tree;f=libs/mapkit/transport/time;hb=HEAD)), чтобы избежать таких ошибок в приложении.
Подробнее в https://wiki.yandex-team.ru/sergejjzhgirovskijj/mobiletimefix/ и https://st.yandex-team.ru/MAPSNAVI-3301

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Калабук (kalabukdima@yandex-team.ru) Алексей Лобанов (allobanov@yandex-team.ru) |
| Отвественные SRE | Алексей Лобанов (allobanov@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/time |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-time/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_TIME |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_time_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_load/) | [ core-time.load ](https://yasm.yandex-team.ru/template/panel/maps-core-time-load-panel-main/) | [ maps_core_time_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_time_load) |
| Prestable | [maps_core_time_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_prestable/) | [ core-time.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-time-prestable-panel-main/) | [ maps_core_time_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_time_prestable) |
| Stable | [maps_core_time_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_stable/) | [ core-time.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-time-stable-panel-main/) | [ maps_core_time_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_time_stable) |
| Testing | [maps_core_time_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_testing/) | [ core-time.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-time-testing-panel-main/) | [ maps_core_time_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_time_testing) |
[Monitorings all (tag=a_prj_maps-core-time)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-time)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-time.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-time.maps.yandex.net/) | [core-time.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-time.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-time-maps;signal=service_total) | [rtc_balancer_core-time_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-time_maps_yandex_net_man)<br>[rtc_balancer_core-time_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-time_maps_yandex_net_sas)<br>[rtc_balancer_core-time_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-time_maps_yandex_net_vla) |

## What happens when service is down
Mapkit не сможет узнать настоящее серверное время, и будет использовать локальное время телефона.

У пользователей, у которых в телефоне установлено неправильное время (например, для их версии системы перестали выходить обновления с таймзонами, пользователи просто поправили часы) прогнозы в остановках будут отличаться от настоящих на эту разницу во времени (например, на час).
Подробнее в https://wiki.yandex-team.ru/sergejjzhgirovskijj/mobiletimefix/ и https://st.yandex-team.ru/MAPSNAVI-3301

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/time/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-time.maps.yandex.net' limit 1;``` |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Core-time - сервис с yacare ручкой, который не использует баз или внешних данных. Ломаться там практически нечему.
Если что-то не так, нужно:
  * Если катится новая версия образа - откатить на старую версию.
  * Иначе, скорее всего, что-то инфраструктурное. Смотреть https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc

## Documentation
https://wiki.yandex-team.ru/sergejjzhgirovskijj/mobiletimefix/

## Known clients
- Mobile-proxy: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config/mapkit2/locations/time.service.conf

## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_time) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_time.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_load/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_time_testing/yp_pods/ |

## Firewall macros
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_TIME_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_TIME_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_TIME_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_TIME_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MTDEV?service=maps-core-time
    * Sandbox:
      * https://sandbox.yandex-team.ru/scheduler/18526
      * https://sandbox.yandex-team.ru/scheduler/18530
    * Тикет: https://st.yandex-team.ru/MTDEV-689
