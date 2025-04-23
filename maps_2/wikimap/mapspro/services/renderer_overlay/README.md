# wiki-renderer-overlay

Рендерер оверлеев для Народной карты (nmaps)

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Евклид Никифоров ( euclid@yandex-team.ru )|
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/renderer_overlay |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-renderer-overlay |
| Проект в CI | [maps-core-nmaps-renderer-overlay](https://a.yandex-team.ru/projects/maps-core-nmaps-renderer-overlay/ci/actions/launches?dir=maps/wikimap/mapspro/services/renderer_overlay) |

## Instances

Сервисы в Няне :
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_renderer_overlay/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_overlay_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_overlay_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_overlay_unstable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_overlay_load/)

## Documentation

NMAPS:
Рендерер оверлеев Народной карты. Используется через https://n.maps.yandex.ru
Отображает в тайлы загруженные изображения с привязкой к координатам и в соответствии с указанным методом трансформации.
Схема API https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/renderer-overlay/api.json

## Known clients

Рендерер - внешний сервисы, доступны через https (открыты порты 80,443)

## ecstatic Datasets

Нет

## What happens when service is down

В Народнай карте не будут отрисовываться подложки в схемах помещений

## Как проверить, что сервис работает

Зайти на https://n.maps.yandex.ru/ - план помещений/уровень. Если к уровню привязяны изображения,
они должны отображаться в тайлы

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

UI :
- Production: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-renderer-overlay.maps.yandex.net/
- Testing: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-renderer-overlay.testing.maps.yandex.net/
- Development: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-nmaps-renderer-overlay-unstable-lsb

Balancers URL :
- Production: https://core-nmaps-renderer-overlay.maps.yandex.ru
- Testing: https://core-nmaps-renderer-overlay.testing.maps.yandex.ru
- Development: https://core-nmaps-renderer-overlay-unstable.maps.n.yandex.ru

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_overlay_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_overlay_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_overlay_unstable |
| Juggler (Load) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_overlay_load |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-renderer-overlay-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-overlay-stable-panel-main) |
| Testing | [maps-core-nmaps-renderer-overlay-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-overlay-testing-panel-main) |
| Unstable | [maps-core-nmaps-renderer-overlay-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-overlay-unstable-panel-main) |
| Load | [maps-core-nmaps-renderer-overlay-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-overlay-load-panel-main) |


## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| wiki-renderer-overlay | /var/log/yandex/maps/wiki-renderer-overlay/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations
