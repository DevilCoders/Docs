# Core Factory Downloader

Сервис для скачивания поставок спутниковых снимков от Diginal Globe и Scanex

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Николай Федоров (unril@yandex-team.ru) Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | [maps/factory/services/downloader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/downloader) |
| Сервис в ABC | [maps-core-factory-downloader](https://abc.yandex-team.ru/services/maps-core-factory-downloader/)|
| CI (TestEnv) - Покоммитный | [BUILD_DOCKER_MAPS_CORE_FACTORY_DOWNLOADER](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_FACTORY_DOWNLOADER/history?limit=20) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_downloader_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_downloader_stable/) | [ core-factory-downloader.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-downloader-stable-panel-main/) | [ maps_core_factory_downloader_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_downloader_stable) |
| Testing | [maps_core_factory_downloader_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_downloader_testing/) | [ core-factory-downloader.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-downloader-testing-panel-main/) | [ maps_core_factory_downloader_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_downloader_testing) |


[Monitorings all (tag=a_prj_maps-core-factory-downloader)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-downloader)


## What happens when service is down

На спутниковую фабрику перестают подгружаться новые поставки.

## Logs
| Name | URL/path |
|---|---|
| DG downloader | /var/log/yandex/maps/factory/downloader/digital-globe.* |
| Scanex downloader | /var/log/yandex/maps/factory/downloader/scanex.* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients



## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_DOWNLOADER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_DOWNLOADER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_DOWNLOADER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_DOWNLOADER_TESTING_RTC_NETS_ ) |


