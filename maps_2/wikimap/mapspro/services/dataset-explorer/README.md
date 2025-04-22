# dataset-explorer

Выдаёт информацию о релизах Народной карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Александр Бобков ( alexbobkov@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/dataset-explorer |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-dataset-explorer/ |
| Проект в CI | [maps-core-nmaps-dataset-explorer](https://a.yandex-team.ru/projects/maps-core-nmaps-dataset-explorer/ci/actions/launches?dir=maps/wikimap/mapspro/services/dataset-explorer) |

## Instances

| Environment | URL |
|---|---|
| Сервисы в няне | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_dataset_explorer_stable/ |
| | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_dataset_explorer_testing/ |
| Dashboard | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_dataset_explorer/ |

## Documentation

Схема: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/dataset-explorer

## Known clients

Garden: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/tools/scan-datastorage

## ecstatic Datasets

Нет

## What happens when service is down

Огород не узнает о новых релизах Народной карты. Они не будут доступны в UI Огорода.

## Как проверить, что сервис работает

Зайти в огород (тестинговый):<br/>
``` ssh `sky list Y@maps_core_garden_scheduler_testing` ```

Сделать http-запрос, обычно страница более 100kb:<br/>
```curl -s http://core-nmaps-dataset-explorer.maps.yandex.net/v0.1/export/ymapsdf | wc -c```

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-dataset-explorer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-dataset-explorer.maps.yandex.net/) | [core-nmaps-dataset-explorer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-dataset-explorer.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla;prj=core-nmaps-dataset-explorer-maps;signal=service_total) | [rtc_balancer_core-nmaps-dataset-explorer_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-dataset-explorer_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-dataset-explorer_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-dataset-explorer_maps_yandex_net_vla) |

Balancers URL:
- Production: http://core-nmaps-dataset-explorer.maps.yandex.net
- Testing: http://core-nmaps-dataset-explorer.common.testing.maps.yandex.net

## Мониторинги

| Type | URL |
|---|---|
| Juggler (all) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_dataset_explorer_stable%7Chost%3Dmaps_core_nmaps_dataset_explorer_testing |
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_dataset_explorer_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_dataset_explorer_testing |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-dataset-explorer-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-dataset-explorer-stable-panel-main) |
| Testing | [maps-core-nmaps-dataset-explorer-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-dataset-explorer-testing-panel-main) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| dataset-explorer | /var/log/yandex/maps/dataset-explorer/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations

Нет
