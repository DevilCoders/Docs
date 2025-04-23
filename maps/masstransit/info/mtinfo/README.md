# maps-core-masstransit-mtinfo
Сервис отдаёт информацию об остановках и маршрутах общественного транспорта, включая ползающие по карте GPS-автобусы. Информацию об автобусах получает от сервиса [maps-core-masstransit-predictor](https://abc.yandex-team.ru/services/maps-core-masstransit-predictor/).

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin), [Андрей Козлов](https://staff.yandex-team.ru/pedeathtrian) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/mtinfo |
| Сервис в ABC | [maps-core-masstransit-mtinfo](https://abc.yandex-team.ru/services/maps-core-masstransit-mtinfo/)|
| Проект в CI | [maps-core-masstransit-mtinfo](https://a.yandex-team.ru/projects/maps-core-masstransit-mtinfo/ci/actions/launches?dir=maps/masstransit/info/mtinfo) |

## Instances

| Environment | URL |
|---|---|
| Сервисы в няне | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_mtinfo_stable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_mtinfo_prestable/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_mtinfo_testing/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_mtinfo_datatesting/|
| |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_mtinfo_load/|
| Dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_masstransit_mtinfo/ |
| Nanny tickets | https://nanny.yandex-team.ru/ui/#/queues/MTDEV/ |

## Documentation

* https://wiki.yandex-team.ru/maps/dev/core/masstransit/gps/
* https://st.yandex-team.ru/MAPSJAMS-3386

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment                       | TVM Application ID
----------------------------------|-------------------
testing                           | [2013396](https://abc.yandex-team.ru/services/maps-core-masstransit-mtinfo/resources/)
datatesting (использует testing)  | [2013396](https://abc.yandex-team.ru/services/maps-core-masstransit-mtinfo/resources/)
production                        | [2013394](https://abc.yandex-team.ru/services/maps-core-masstransit-mtinfo/resources/)


## Known clients

* %maps_int - https://c.yandex-team.ru/groups/maps_int
* Mobile-proxy
  * https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config/mapkit2/
  * https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config/transport
* mobile/legacy/printer - https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/legacy/printer/fastcgi-conf/src
* MAPS_MASSTRANSIT_JUMP_COUNTER - https://sandbox.yandex-team.ru/schedulers?task_type=MAPS_MASSTRANSIT_JUMP_COUNTER


## Ecstatic Datasets
| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) | [yandex-maps-masstransit-data](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions) |
| [yandex-maps-masstransit-regions-config-production](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-regions-config-production/versions) | [yandex-maps-masstransit-regions-config](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-regions-config/versions) | [yandex-maps-masstransit-regions-config-datatesting](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-regions-config-datatesting/versions) |
| [yandex-maps-geodata5](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata5/versions) | [yandex-maps-geodata5](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geodata5/versions) |
| [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |
| [yandex-maps-masstransit-predictions](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions) | [yandex-maps-masstransit-predictions](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions) | [yandex-maps-masstransit-predictions](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions) |

## Sandbox resources
В mtinfo есть sandbox-ресурсы, которые обновляет nanny-робот. Обновления, которые сейчас выполняет робот, можно видеть в тикетной очереди https://nanny.yandex-team.ru/ui/#/queues/MTDEV/ , а также в dashboard-е.
* vehicle_properties - свойства автобусов (низкопольность)
  * https://sandbox.yandex-team.ru/resources/?type=MAPS_MASSTRANSIT_VEHICLE_PROPERTIES
  * обновляется раз в день: https://sandbox.yandex-team.ru/scheduler/9685/view
* masstransit-regions.conf - серверный конфиг с регионами, в которых показывать метки и прогнозы
  * https://sandbox.yandex-team.ru/resources/?type=MAPS_MASSTRANSIT_REGIONS_CONFIG_PRODUCTION
  * https://sandbox.yandex-team.ru/resources/?type=MAPS_MASSTRANSIT_REGIONS_CONFIG_TESTING
  * https://sandbox.yandex-team.ru/resources/?type=MAPS_MASSTRANSIT_REGIONS_CONFIG_DATATESTING
  * обновляется по коммиту - https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/masstransit/UpdateRegionsConfig.yaml


## What happens when service is down
Клиенты перестают видеть метки ОТ на карте.
Не получают информацию при клике на остановку или на метку, которая успела попасть на клиент.

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/maps/dev/core/Instrukcija-po-sozdaniju-servisov-v-RTC/whatcangowronginrtc/)

How to restart service
  * Чтобы переподнять контейнер, используйте Instances->State в nanny. Дёргать вручную yacare restart/reload не рекомендуется - [подробнее](https://wiki.yandex-team.ru/maps/dev/core/Instrukcija-po-sozdaniju-servisov-v-RTC/whatcangowronginrtc/#javsepochinilcherezyacarerestartvsezarabotaloapotomopjatslomalos).

Горит мониторинг maps-ecstatic-*
  * Поискать такой случай https://wiki.yandex-team.ru/maps/dev/core/ecstatic/#monitoringchecks
  * Звать на помощь geo-infra

Не переключаются данные в ecstatic:
  * Посмотреть статус и ошибки в http://ecstatic.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions и/или http://ecstatic.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions (в зависимости от используемых данных)
  * Посмотреть лог ecstatic-agent-а /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log
  * Если ошибка во время switch, и она разовая, можно "подтолкнуть" версию ещё раз с помощью Sandbox-таски MAPS_ECSTATIC_DATASET_MANAGER https://sandbox.yandex-team.ru/task/273503453/view
  * Посмотреть, качаются ли торренты: /var/run/yandex/maps/ecstatic/ymtorrent.status
  * Звать на помощь geo-infra
  * (Advanced) Если не происходит switch, но в ecstatic-agent.log ничего нет:
    * Проверить времена файлов в /var/run/yandex/maps/ecstatic/ - там можно увидеть когда worker успешно запускался и успешно завершался
    * Запустить worker вручную /usr/lib/yandex/maps/ecstatic/worker.sh и посмотреть, на что он ругается.

На клиентах не отображаются метки или прогнозы, но мониторинги молчат
  * Проверить мониторинги [mtpredictor](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mtpredictor/)
  * https://wiki.yandex-team.ru/RomanUdovichenko/MT/whattodo/#netmetok

## Балансеры
Balancers URL:
Production: http://core-masstransit-mtinfo.maps.yandex.net
Testing: http://core-masstransit-mtinfo.common.testing.maps.yandex.net
Datatesting: http://core-masstransit-mtinfo.common.datatesting.maps.yandex.net

* Production:
  * Nanny-сервисы l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-mtinfo_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-mtinfo_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-mtinfo_maps_yandex_net_vla/
  * AWACS-балансеры: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-masstransit-mtinfo.maps.yandex.net/show/
  * Мониторинг: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-masstransit-mtinfo_maps_yandex_net_*&statuses=CRIT%2CWARN%2COK
  * Настройки файрвола: https://puncher.yandex-team.ru/?destination=core-masstransit-mtinfo.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

* Testing: общий карточный балансер common.testing.maps.yandex.net
* Datatesting: общий карточный балансер common.datatesting.maps.yandex.net

## Мониторинги
| Type                         | URL                                                                                                                                                                                                           |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Juggler (all)                | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_mtinfo_*> |
| Juggler (stable)             | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_mtinfo_stable>                                                                                                 |
| Juggler (prestable)          | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_mtinfo_prestable>                                                                                                 |
| Juggler (testing)            | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_mtinfo_testing>                                                                                                          |
| Juggler (datatesting)        | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_mtinfo_datatesting>                                                                                                      |

Настройки SEDEM: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/mtinfo/sedem_config

## Графики
| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-mtinfo;ctype=prestable,stable/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-mtinfo;ctype=testing/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;prj=maps-core-masstransit-mtinfo;ctype=datatesting/>      |

Настройки - в общем шаблоне для masstransit в RTC: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/configs/yasm/panels

SEDEM панели

| Type                         | URL                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Golovan (prestable + stable) | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-mtinfo-stable-panel-main/> |
| Golovan (testing)            | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-mtinfo-testing-panel-main/>          |
| Golovan (datatesting)        | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-mtinfo-datatesting-panel-main/>      |
| Ratelimiter                  | <https://yasm.yandex-team.ru/template/panel/maps_core_masstransit_mtinfo-ratelimiter2-panel>        |

## SLA

[Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_mtinfo)
[Определение проверки в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_masstransit_mtinfo.py)


## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Mtinfo | /var/log/yandex/maps/mtinfo/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru/Operations/W09B6Da9vESCNGE6Jn03drcymW2vpTfPDsacsaf4iDQ= |
|     | SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2018-07-17] WHERE vhost = 'core-masstransit-mtinfo.maps.yandex.net'; |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Lunapark charts | <https://lunapark.yandex-team.ru/regress/MTDEV?service=Mtinfo> |
| Sandbox Scheduler | <https://sandbox.yandex-team.ru/scheduler/11959/view> |
| Sandbox Task | <https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtinfoShooting/__init__.py> |
