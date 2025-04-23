# wiki-renderer

Рендерер Народной карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Алексей Пономарев ( ponomarev@yandex-team.ru ) Евклид Никифоров ( euclid@yandex-team.ru ) Борис Чикунов ( chikunov@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/renderer |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-renderer-nmaps/ |
| Проект в CI | [maps-core-nmaps-renderer-nmaps](https://a.yandex-team.ru/projects/maps-core-nmaps-renderer-nmaps/ci/actions/launches?dir=maps/wikimap/mapspro/services/renderer) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_renderer_nmaps/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_nmaps_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_nmaps_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_nmaps_unstable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_renderer_nmaps_load/)

## Documentation

Рендерер Народной карты для внешних пользователей.
Используется из https://n.maps.yandex.ru/ и https://npro.maps.yandex.ru/ (внутренняя сеть)

## Known clients

Рендерер - внешний сервис, доступен через https (открыты порты 80,443)

Мобильное приложение "Народная Карта" использует ручку `/tile`

- wiki-renderer -> `_PGAASINTERNALNETS_`:6432
- wiki-renderer -> core-nmaps-editor.maps.yandex.net:80

## ecstatic Datasets

Нет

## What happens when service is down

Народная карта (nmaps) не будет работать
В мобильном приложении "Народная карта" не будут отображаться векторные тайлы на экране пешеходного сценария

## Как проверить, что сервис работает

Зайти на https://n.maps.yandex.ru/ - должны отображаться тайлы

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

UI:
- Production: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-renderer-nmaps.maps.yandex.net/show/
- Testing: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-renderer-nmaps.testing.maps.yandex.net/show/
- Development: https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-nmaps-renderer-nmaps-unstable-slb

Balancers URL:
- Production: https://core-nmaps-renderer-nmaps.maps.yandex.net
- Testing: https://core-nmaps-renderer-nmaps.testing.maps.yandex.net
- Development: https://core-nmaps-renderer-nmaps-unstable.maps.n.yandex.ru

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_nmaps_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_nmaps_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_nmaps_unstable |
| Juggler (Load) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_renderer_nmaps_load |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-renderer-nmaps-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-nmaps-stable-panel-main) |
| Testing | [maps-core-nmaps-renderer-nmaps-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-nmaps-testing-panel-main) |
| Unstable | [maps-core-nmaps-renderer-nmaps-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-nmaps-unstable-panel-main) |
| Load | [maps-core-nmaps-renderer-nmaps-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-renderer-nmaps-load-panel-main) |
| mapspro_view_trunk | [mapspro_view_trunk](https://yasm.yandex-team.ru/panel/chikunov.mapspro_view_trunk) |
| mapspro_view_trunk_labels | [mapspro_view_trunk_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbsj61vh1ob68181o6v;dbname=mapspro_view_trunk_labels) |
| mapspro_view_stable | [mapspro_view_stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbe9n7jsv7p2rih4na2;dbname=mapspro_view_stable) |
| mapspro_view_stable_labels | [mapspro_view_stable_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb8dsn266l6muu3pgsm;dbname=mapspro_view_stable_labels) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| wiki-renderer | /var/log/yandex/maps/wiki-renderer/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/NMAPS?service=Renderer)
- [Scheduler for imbalance shootings, production log](https://sandbox.yandex-team.ru/scheduler/14114/view)
- [Scheduler for timing shootings, production log](https://sandbox.yandex-team.ru/scheduler/14115/view)
- [Scheduler for imbalance shootings, zoom 1..7](https://sandbox.yandex-team.ru/scheduler/14139/view)
- [Scheduler for timing shootings, zoom 1..7](https://sandbox.yandex-team.ru/scheduler/14140/view)
- [Scheduler for imbalance shootings, zoom 8..11](https://sandbox.yandex-team.ru/scheduler/14142/view)
- [Scheduler for timing shootings, zoom 8..11](https://sandbox.yandex-team.ru/scheduler/14143/view)
- [Scheduler for imbalance shootings, zoom 12..14](https://sandbox.yandex-team.ru/scheduler/14146/view)
- [Scheduler for timing shootings, zoom 12..14](https://sandbox.yandex-team.ru/scheduler/14147/view)
- [Scheduler for imbalance shootings, zoom 15..21](https://sandbox.yandex-team.ru/scheduler/14154/view)
- [Scheduler for timing shootings, zoom 15..21](https://sandbox.yandex-team.ru/scheduler/14155/view)
