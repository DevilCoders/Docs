# Maps-Core-Ecstatic-Coordinator

Manages the distribution of datasets to various groups of machines. Part of Ecstatic.

## Graphs
| Staging | URL |
|---|---|
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-coordinator-stable-panel-main/ |
| Prestable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-coordinator-prestable-panel-main/ |
| Datatesting | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-coordinator-datatesting-panel-main/ |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-coordinator-testing-panel-main/ |
| Unstable | https://yasm.yandex-team.ru/template/panel/maps-core-ecstatic-coordinator-unstable-panel-main/ |
| Databases | https://grafana.yandex-team.ru/d/000008820/ecstatic?orgId=1 |

## General information

| Topic | Information |
|---|---|
| Responsible developers | Алексей Хроленко (khrolenko@yandex-team.ru) Никита Оскотский (nikitonsky@yandex-team.ru) |
| Responsible SRE | Алексей Хроленко (khrolenko@yandex-team.ru) Иван Селезнев (imseleznev@yandex-team.ru) |
| Packages | yandex-maps-ecstatic-client, yandex-maps-ecstatic-common, yandex-maps-ecstatic-conf-maps, yandex-maps-ecstatic-coordinator, yandex-maps-ecstatic-storage, yandex-maps-ecstatic-tool |
| Configuration | https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ecstatic/coordinator |
| ABC service | https://abc.yandex-team.ru/services/maps-core-ecstatic-coordinator |
| CI (TestEnv) | https://beta-testenv.yandex-team.ru/project/maps_geoinfra_tests/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_ECSTATIC_COORDINATOR/history |

## Instances

| Environment | URL |
|---|---|
| Nanny services | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_testing|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_prestable|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_stable|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_datatesting|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_load|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ecstatic_coordinator_unstable|
| Dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_ecstatic_coordinator|

## Documentation
- https://wiki.yandex-team.ru/maps/dev/core/ecstatic/
- https://wiki.yandex-team.ru/maps/dev/core/ecstatic/impl/httpapi
- https://wiki.yandex-team.ru/maps/dev/core/ecstatic/impl/db-schema

## What happens when the service is down

All the services that depend on data delivery by Ecstatic stop getting fresh data.

Прекращается прием новых данных от пользователей и синхронизация версий в группах.
Деградации:
- Freeze mode -- остановка синхронизации версий и управления данными на клиентах. Включается вручную.
- Потеря стораждей -- приводит к уменьшению отказоустойчивости. При невозможности репликации, загрузка данных на сторадж прекращается.
- Потеря фастбона -- значительно усложняет обработку больших объемов данных.
- Проблемы с конфигурацией -- изменения в составах групп, инвалидирующие текущую конфигурацию, или недоступность источника данных (Кондуктор, Qloud). Приводит к фиксации последней успешной конфигурации.

## How to fix common issues

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

В первую очередь смотрим на графиках (см. выше) 500-ки или 499-ки на координаторе - если есть массовые проблемы, то чинить нужно их. Ищем резкие скачки на графиках, проверяем нагрузку и трафик на mongodb. Повышенная load average на машинке может быть вызвана соседней виртуалкой. Если с монгой все хорошо, но 500-ки на координаторе остаются, пробуем перезагрузить координатор
yacare restart ecstatic-coordinator
Если проблемы остаются, изучаем логи nginx-а и /var/log/yandex/maps/ecstatic-coordinator/ecstatic-coordinator.log
При недавних выкатках пакета yandex-maps-ecstatic-coordinator откатываем его на прошлую версию.
При задержках выкатки какого-либо датасета ищем этот датасет на страничке статусов:
- тестинг - http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/list
- стейбл - http://core-ecstatic-coordinator.maps.yandex.net/pkg/list

Unknown - на машинке не запущен ymtorrent или нет дырок до координатора
Downloaded - данные скачались, но не прошел posdl-хук
Ready - postdl прошел, но не набрался кворум для активации, или не отработал switch-хук
Disabled - версия датасета не была мувнута в ту ветку, для которой определён деплой на этот хост
Идем на проблемную машинку и проверяем:
- В файле /etc/yandex/maps/ecstatic/conf задан правильный инстанс координатора и на него можно сходить curl-ом
- На машинке есть свободное место
- Запущен ymtorrent и на него можно сходить с помощью curl localhost:9246 . Если ymtorrent присутствует в списке процессов, но не отвечает на curl, то желательно снять корку с помощью gcore <ymtorrent_pid> и написать Алексей Хроленко. Далее kill -9 <ymtorrent_pid> .
- Если место на диске и сеть присутствуют, перезагружаем клиента service ecstatic-client restart . Для storage-машинок - service ecstatic-storage restart .
- Смотрим на вывод ip addr . Если у eth0 два глобальных IP адреса, тогда тот, что dynamic, нужно удалить ip addr del <ipv6 addres>/64 dev eth0 . Скорее всего IP появился после ребута машинки (можно проверить по uptime). Так же нужно не забыть проверить, что accept_ra = 0: sysctl net.ipv6.conf.eth0.accept_ra . После удаления IP желательно проверить что все получилось повторным ip addr
- Если ничего не помогло, смотрим логи /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log
- Проверьте, что версии установленных пакетов ecstatic и yandex-maps-torrent-client совпадают с априори исправной машинкой в том же окружении.

See also: [Monitoring checks](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#monitoringchecks)

## Balancers
### Production:
- Porto metrics for the balancer container: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-ecstatic-coordinator.maps.yandex.net;prj=maps-core-ecstatic-coordinator;ctype=prestable,stable;hosts=ASEARCH;itype=maps
- Generated Nanny services for the L7 balancers:
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_maps_yandex_net_man
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_maps_yandex_net_sas
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_maps_yandex_net_vla
- Generated AWACS balancers:
   - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ecstatic-coordinator.maps.yandex.net
- Link to the farm in L3 manager:
   - https://l3.tt.yandex-team.ru/service/4154
- Firewall setup: https://puncher.yandex-team.ru/?destination=core-ecstatic-coordinator.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Firewall setup modifications through the puncher service: https://puncher.yandex-team.ru
- Balancers monitoring: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-ecstatic-coordinator_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-ecstatic-coordinator_maps_yandex_net_sas|host%3Drtc_balancer_core-ecstatic-coordinator_maps_yandex_net_man&last=1DAY

### Datatesting:
- Porto metrics for the balancer container: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-ecstatic-coordinator.datatesting.maps.yandex.net;prj=maps-core-ecstatic-coordinator;ctype=testing;hosts=ASEARCH;itype=maps
- Generated Nanny services for the L7 balancers:
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_man
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_sas
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_vla
- Generated AWACS balancers:
   - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ecstatic-coordinator.datatesting.maps.yandex.net
- Link to the farm in L3 manager:
   - https://l3.tt.yandex-team.ru/service/8246
- Firewall setup: https://puncher.yandex-team.ru/?destination=core-ecstatic-coordinator.datatesting.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Firewall setup modifications through the puncher service: https://puncher.yandex-team.ru
- Balancers monitoring: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_sas%7Chost%3Drtc_balancer_core-ecstatic-coordinator_datatesting_maps_yandex_net_man&last=1DAY

### Testing:
- Porto metrics for the balancer container: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-ecstatic-coordinator.testing.maps.yandex.net;prj=maps-core-ecstatic-coordinator;ctype=testing;hosts=ASEARCH;itype=maps
- Generated Nanny services for the L7 balancers:
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_man
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_sas
    - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_vla
- Generated AWACS balancers:
   - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ecstatic-coordinator.testing.maps.yandex.net
- Link to the farm in L3 manager:
   - https://l3.tt.yandex-team.ru/service/3377
- Firewall setup: https://puncher.yandex-team.ru/?destination=core-ecstatic-coordinator.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination
- Firewall setup modifications through the puncher service: https://puncher.yandex-team.ru
- Balancers monitoring: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_sas%7Chost%3Drtc_balancer_core-ecstatic-coordinator_testing_maps_yandex_net_man&last=1DAY

### Unstable:
- This staging is managed by the service balancer: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-ecstatic-coordinator-unstable-slb

### Balancers URLs:
- Production and prestable: http://core-ecstatic-coordinator.maps.yandex.net
- Datatesting: http://core-ecstatic-coordinator.datatesting.maps.yandex.net
- Testing: http://core-ecstatic-coordinator.testing.maps.yandex.net
- Unstable: http://core-ecstatic-coordinator.common.unstable.maps.yandex.net

## Monitoring
| Staging | URL |
|---|---|
| Stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_coordinator_stable |
| Prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_coordinator_prestable |
| Datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_coordinator_datatesting |
| Testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_coordinator_testing |
| Unstable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ecstatic_coordinator_unstable |

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_ECSTATIC_COORDINATOR_STABLE_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ECSTATIC_COORDINATOR_STABLE_RTC_NETS_ ) |
| datatesting | [ \_MAPS_CORE_ECSTATIC_COORDINATOR_DATATESTING_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ECSTATIC_COORDINATOR_DATATESTING_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_ECSTATIC_COORDINATOR_TESTING_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ECSTATIC_COORDINATOR_TESTING_RTC_NETS_ ) |

## Setting up a monitor

https://wiki.yandex-team.ru/geo-infra/SEDEM/

## SLA

[stat report](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_ecstatic_coordinator)

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Coordinator | /var/log/yandex/maps/ecstatic-coordinator/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : USE hahn; SELECT * FROM [logs/maps-log/1d/2018-09-20] WHERE tskv_format='ecstatic-coordinator'; |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/GEOINFRA?service=ecstatic-coordinator |
| CI (imbalance) | https://sandbox.yandex-team.ru/scheduler/702184/view |
| CI (timings) | TODO |

## Mongo charts

| Env | | |
|---|---|---|
| unstable | [mdb](https://yc.yandex-team.ru/folders/fooi8oggs4322na3n2l1/managed-mongodb/cluster/mdbu9potf26q3i3b0d4l?section=monitoring) | [yasm](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=mdbu9potf26q3i3b0d4l) |
| testing | [mdb](https://yc.yandex-team.ru/folders/fooi8oggs4322na3n2l1/managed-mongodb/cluster/mdbgtnk85h14eoev3r2b?section=monitoring) | [yasm](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=mdbgtnk85h14eoev3r2b) |
| datatesting | [mdb](https://yc.yandex-team.ru/folders/fooi8oggs4322na3n2l1/managed-mongodb/cluster/mdbfns3tok9e7n5kf18c?section=monitoring) | [yasm](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=mdbfns3tok9e7n5kf18c) |
| stable | [mdb](https://yc.yandex-team.ru/folders/fooi8oggs4322na3n2l1/managed-mongodb/cluster/mdb9sketa7ile8ndmjse?section=monitoring) | [yasm](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=mdb9sketa7ile8ndmjse) |
| load | [mdb](https://yc.yandex-team.ru/folders/fooi8oggs4322na3n2l1/managed-mongodb/cluster/mdb509pg0gm90rij0eij?section=monitoring) | [yasm](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=mdb509pg0gm90rij0eij) |


## Backups
[wiki](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#backup)

Добавление прав для работы с s3 mds делается на основе [wiki](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys)

Полученные access_key_id/secret нужно положить в [yav](https://yav.yandex-team.ru/secret/sec-01dpkcv9kxzkyj0tacsf7pvbbm/explore/versions)
и в sandbox vault MAPS_ECSTATIC_BACKUPPER_S3_CREDENTIALS_TOKEN
