# road_graph_deployment

## Module description
This module activates road graph deployment.

Deployment activation is somehow autostarted but only according to the timetable.

The autostarter can be enabled/disabled according [the instruction](https://wiki.yandex-team.ru/users/kmkolganov/roadgraphdeployment).

## Откат графа на предыдущую версию

Так как активация графа содержит этап 2-х часового ожидания между prestable и stable ветками ecstatic, то нам нужен механизм активации в stable-ветке без ожидания.

План действий.
1. Перейдите на страницу [модуля в Огороде](https://garden.maps.yandex-team.ru/stable/road_graph_deployment).
2. Выберите версию графа, на которую хотите откатиться, например, _20.09.02-01_.
3. Запустите через UI Огорода активацию этой версии.
4. Дождитесь, когда все датасеты активируются в ветке prestable. Это можно проверить в ecstatic, а также [на странице активных YT-операций Огорода](http://core-garden-server.maps.yandex.net/yt_monitor?module=road_graph_deployment) должна исполняться таска _WaitNecessaryTimeTask.
5. Убедитесь, что в dataprestable проблем нет.
6. Для ручной активации в ветке stable зайдите на какую-нибудь [stable-машину роутера](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_router_stable) по ssh.
7. Выполните на этой машине последовательно команды активации `ecstatic move <dataset-name>=<version> +stable`, например, `ecstatic move yandex-maps-graph-compact=20.09.02-01 +stable` в следующей последовательности:
* yandex-maps-graph-compact
* yandex-maps-graph-compact-rtree
* yandex-maps-graph-compact-edges-persistent-index
* yandex-maps-graph-activator,
* yandex-maps-graph-data,
* yandex-maps-graph-router-compact-data7,
* yandex-maps-graph-router-data7,
* yandex-maps-graph-router-experimental-speeds-diff,
* yandex-maps-graph-router-topology7,
* yandex-maps-graph-routing-barriers-rtree,
* yandex-maps-graph-segments-rtree,
* yandex-maps-graph-topology,
* yandex-maps-graph-router-carparks,
* yandex-maps-graph-edges-persistent-index,
* yandex-maps-graph-compact-edges-persistent-index,
* yandex-maps-graph-activator
8. Убедившись в координаторе ecstatic, что версия yandex-maps-graph-activator активна везде, нужно выполнить активацию в ветке stable следующих датасетов:
* yandex-maps-mobile-driving-config-data
* yandex-maps-mobile-driving-config-dataprestable
* yandex-maps-graph-closures

Для выполнения пунктов 7 и 8 можно воспользоваться [сценарием на Python-е](https://st.yandex-team.ru/MAPSNAVI-5844/attachments/22818459?activate_graph.py).