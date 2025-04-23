# Core Factory Lt

Воркеры для выполнения асинхронных задач

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE |  |
| Исходники | [maps/factory/services/lt](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/lt) |
| Сервис в ABC | [maps-core-factory-lt](https://abc.yandex-team.ru/services/maps-core-factory-lt/)|
| CI (TestEnv) - Покоммитный | https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_FACTORY_LT/history?limit=20 |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_lt_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_lt_stable/) | [ core-factory-lt.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-lt-stable-panel-main/) | [ maps_core_factory_lt_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_lt_stable) |
| Testing | [maps_core_factory_lt_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_lt_testing/) | [ core-factory-lt.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-lt-testing-panel-main/) | [ maps_core_factory_lt_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_lt_testing) |


[Monitorings all (tag=a_prj_maps-core-factory-lt)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-lt)


[Coredumps](https://coredumps.n.yandex-team.ru/index?text_to_search=&itype=core-factory-lt-stable&ctype_list=&prj_list=&tag_list=&host_list=&signal=)

## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Workers | /var/log/yandex/maps/factory/grinder/ |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_LT_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_LT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_LT_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_LT_TESTING_RTC_NETS_ ) |
