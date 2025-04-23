# Core Search Menu
Сервис выдаёт список рекламных категорий для заданных menu_page_id, положения пользователя и языка

[Wiki-страница с более подробной информацией](https://wiki.yandex-team.ru/users/folunin/core-search-menu/)

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Виктор Теплов (grok@yandex-team.ru) <br> Владимир Фолунин (folunin@yandex-team.ru) |
| Отвественные SRE | Владимир Фолунин (folunin@yandex-team.ru) |
| Исходники | [maps/search/menu](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/menu) |
| Сервис в ABC | [maps-core-search-menu](https://abc.yandex-team.ru/services/maps-core-search-menu/)|
| CI (TestEnv) | [BUILD_DOCKER_MAPS_CORE_SEARCH_MENU](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_SEARCH_MENU/history?limit=20)|

## Usage

### Balancers

* Stable — core-search-menu.maps.yandex.net
* Testing — core-search-menu.common.testing.maps.yandex.net

### Endpoints
`/menu`

Возвращает список категорий (MenuItem) для заданной площадки и заданного языка, геометрия которых содержит заданную точку, а расписание (Schedule), если оно есть, содержит текущий момент времени.

Параметры:
* `menu_page_id`  — идентификатор площадки (МЯК, Нави и т. п.); будут возвращены только те категории, у которых Platform id совпадает с указанным;
* `lang`  — язык; у возвращаемых категорий будут выбраны соответствующие title/subtitle;
* `ll`  — положение пользователя (долгота и широта); будут возвращены только те категории, у которых заданная точка входит в геометрию;
* `hr`  — возвращать человекочитаемый ответ.

Пример запроса в testing: https://core-search-menu.common.testing.maps.yandex.net/menu?menu_page_id=mobile_maps_search&lang=ru&ll=37.5,55.6&hr=yes

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_core_search_menu_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_search_menu_prestable/) | [maps_core_search-menu.prestable](https://yasm.yandex-team.ru/template/panel/maps-core-search-menu-prestable-panel-main/) | [maps_core_search_menu_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_search_menu_prestable) |
| Stable | [maps_core_search_menu_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_search_menu_stable/) | [ core-search-menu.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-search-menu-stable-panel-main/) | [ maps_core_search_menu_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_search_menu_stable) |
| Testing | [maps_core_search_menu_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_search_menu_testing/) | [ core-search-menu.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-search-menu-testing-panel-main/) | [ maps_core_search_menu_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_search_menu_testing) |

[Monitorings all (tag=a_prj_maps-core-search-menu)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-search-menu)

### Balancers
| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-search-menu.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-search-menu.maps.yandex.net/) | [core-search-menu.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-search-menu.maps.yandex.net;itype=balancer;ctype=prod;locations=;prj=core-search-menu-maps;signal=service_total) | [rtc_balancer_core-search-menu_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-search-menu_maps_yandex_net_man) <br> [rtc_balancer_core-search-menu_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-search-menu_maps_yandex_net_sas) <br> [rtc_balancer_core-search-menu_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-search-menu_maps_yandex_net_vla) |

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/search-menu/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : `USE chyt.hahn; SELECT * FROM "//logs/maps-log/1d/2021-03-16" WHERE vhost='core-search-menu.maps.yandex.net' LIMIT 1;` |

## Firewall macros

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_SEARCH_MENU_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SEARCH_MENU_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_SEARCH_MENU_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SEARCH_MENU_TESTING_RTC_NETS_ ) |

## Known clients
* [Maps Core Mobile Proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy)
