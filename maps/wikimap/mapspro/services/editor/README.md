# wiki-editor

Редактор Народной карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Евклид Никифоров ( euclid@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/editor |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-editor/ |
| Сервис в ABC (writer) | https://abc.yandex-team.ru/services/maps-core-nmaps-editor-writer/ |
| Проект в CI (reader) | [maps-core-nmaps-editor](https://a.yandex-team.ru/projects/maps-core-nmaps-editor/ci/actions/launches?dir=maps/wikimap/mapspro/services/editor/reader) |
| Проект в CI (writer) | [maps-core-nmaps-editor-writer](https://a.yandex-team.ru/projects/maps-core-nmaps-editor-writer/ci/actions/launches?dir=maps/wikimap/mapspro/services/editor/writer) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_editor/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_editor_stable/)
- [stable writer](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_editor_writer_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_editor_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_editor_unstable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_editor_load/)

## Documentation

Схема: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/editor

## Known clients

https://puncher.yandex-team.ru/?destination=core-nmaps-editor.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

wiki-editor -> `_PGAASINTERNALNETS_`:6432
wiki-editor -> feedback-int.c.maps.yandex.net:80

`_MAPSPRODQNETS_`,`_MAPSNETS_`,`_ALTAY_BACK_PROD_NETS_`,`_SEARCHHITMANNETS_` -> wiki-editor:80

## ecstatic Datasets

Нет

## What happens when service is down

Единая и Народная карты не будут работать

## Как проверить, что сервис работает

Сделать запрос с какой-нибудь из машин %maps_um_lt
executer> exec %maps_um_lt curl -v http://core-nmaps-editor.maps.yandex.net/ping 2>&1 |grep 200

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable (reader) | default | [core-nmaps-editor.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-editor.maps.yandex.net/) | [core-nmaps-editor.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=core-nmaps-editor.maps.yandex.net;prj=core-nmaps-editor-maps;signal=service_total;) | [rtc_balancer_core-nmaps-editor_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-editor_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-editor_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-editor_maps_yandex_net_vla) |
| Stable (writer) | default | [core-nmaps-editor-writer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-editor-writer.maps.yandex.net/) | [core-nmaps-editor-writer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-nmaps-editor-writer.maps.yandex.net;prj=core-nmaps-editor-writer-maps;signal=service_total;) | [rtc_balancer_core-nmaps-editor-writer_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-editor-writer_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-editor-writer_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-editor-writer_maps_yandex_net_vla) |
| Testing | common_default | [core-nmaps-editor.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-editor.common.testing.maps.yandex.net"}) | [core-nmaps-editor.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-nmaps-editor_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |
| Unstable | common_default | [core-nmaps-editor.common.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.unstable.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-editor.common.unstable.maps.yandex.net"}) | [core-nmaps-editor.common.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.unstable.maps.yandex.net;prj=common.unstable.maps.yandex.net;signal=core-nmaps-editor_common_unstable_maps_yandex_net;) | [rtc_balancer_common_unstable_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_sas) <br>[rtc_balancer_common_unstable_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_man) <br>[rtc_balancer_common_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_vla) |

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_editor_stable |
| Juggler (Production, writer) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_editor_writer_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_editor_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_editor_unstable |
| Juggler (Load) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_editor_load |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Базы данных

Все postgresql-кластеры можно увидеть в MDB в фолдере [foodd8k45ru3cjjo3nte](https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-postgresql).

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-editor-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-editor-stable-panel-main) |
| Stable (writer) | [maps-core-nmaps-editor-writer-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-editor-writer-stable-panel-main) |
| Testing | [maps-core-nmaps-editor-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-editor-testing-panel-main) |
| Unstable | [maps-core-nmaps-editor-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-editor-unstable-panel-main) |
| Load | [maps-core-nmaps-editor-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-editor-load-panel-main) |
| mapspro_core | [mapspro_core](https://yasm.yandex-team.ru/panel/chikunov.mapspro_core/) |
| mapspro_social | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |
| mapspro_view_trunk | [mapspro_view_trunk](https://yasm.yandex-team.ru/panel/chikunov.mapspro_view_trunk) |
| mapspro_view_trunk_labels | [mapspro_view_trunk_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbsj61vh1ob68181o6v;dbname=mapspro_view_trunk_labels) |
| mapspro_view_stable | [mapspro_view_stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbe9n7jsv7p2rih4na2;dbname=mapspro_view_stable) |
| mapspro_view_stable_labels | [mapspro_view_stable_labels](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb8dsn266l6muu3pgsm;dbname=mapspro_view_stable_labels) |
| mapspro_validation | [mapspro_validation](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3aee79ba-6480-4d9d-88d8-020585c701b3;dbname=mapspro_validation) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| wiki-editor | /var/log/yandex/maps/wiki-editor/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/NMAPS?service=Editor)
- [Scheduler for imbalance shootings, comments stat](https://sandbox.yandex-team.ru/scheduler/14437/view)
- [Scheduler for timing shootings, comments stat](https://sandbox.yandex-team.ru/scheduler/14438/view)
- [Scheduler for imbalance shootings, tile](https://sandbox.yandex-team.ru/scheduler/14441/view)
- [Scheduler for timing shootings, tile](https://sandbox.yandex-team.ru/scheduler/14442/view)

## Патч в DNS для UI
core-nmaps-editor.load.maps.yandex.net is an alias for  **YP-POD from maps_core_nmaps_editor_load**

Можно получить динамически из [API Няни](https://nanny.yandex-team.ru/v2/services/maps_core_nmaps_editor_load/current_state/instances/)
