# Core Garden Scheduler

Шедьюлер Огорода - оркеструет сборку данных огородными модулями в YT.
Также содержит ряд вспомогательных демонов и кроновских задач.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Бобков (alexbobkov@yandex-team.ru) |
| Отвественные SRE | Александр Бобков (alexbobkov@yandex-team.ru) |
| Исходники | [maps/garden/scheduler](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler) |
| Сервис в ABC | [maps-core-garden](https://abc.yandex-team.ru/services/maps-core-garden/)|
| CI | https://a.yandex-team.ru/projects/maps-core-garden/ci/actions/launches?dir=maps/garden/scheduler&id=build |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_garden_scheduler_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_garden_scheduler_stable/) | [ core-garden-scheduler.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-garden-scheduler-stable-panel-main/) | [ maps_core_garden_scheduler_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_garden_scheduler_stable) |
| Testing | [maps_core_garden_scheduler_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_garden_scheduler_testing/) | [ core-garden-scheduler.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-garden-scheduler-testing-panel-main/) | [ maps_core_garden_scheduler_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_garden_scheduler_testing) |


[Monitorings all (tag=a_prj_maps-core-garden-scheduler)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-garden-scheduler)


### MDB Mongo clusters

| Staging | MDB cluster |
| ------- | ----------- |
| stable | [cluster](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-mongodb/cluster/mdbgovfcc6lo1thpd2ke) |
| testing | [cluster](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-mongodb/cluster/mdbj0vjs787pnuhr77s2) |


## What happens when service is down

Сборка данных в YT не происходит. Билды в Огороде не запускаются. Нельзя откатить плохие данные из продакшена.

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Garden | /var/log/yandex/maps/garden/* |


## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[Инструкция в документации Огорода](https://docs.yandex-team.ru/garden/garden_duty)


## Documentation

[Документация](https://docs.yandex-team.ru/garden/)


## Persistent Volumes

* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/garden/isolated_modules/cache/ - кэш огородных модулей
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_GARDEN_SCHEDULER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GARDEN_SCHEDULER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_GARDEN_SCHEDULER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GARDEN_SCHEDULER_TESTING_RTC_NETS_ ) |
