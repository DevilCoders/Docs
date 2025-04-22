# Core Renderer Tilemill Serv

Сервис, отдающий vec3 тайлы из тайлсетов, созданных TileMill и хранящихся в S3-MDS.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Евгений Акимов (eak1mov@yandex-team.ru) <br> Андрей Власюк (avlasyuk@yandex-team.ru) |
| Отвественные SRE | Евгений Акимов (eak1mov@yandex-team.ru) |
| Исходники | [maps/renderer/tilemill/serv](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilemill/serv) |
| Сервис в ABC | [maps-core-renderer-tilemill](https://abc.yandex-team.ru/services/maps-core-renderer-tilemill/)|
| Проект в CI | [maps-core-renderer-tilemill](https://a.yandex-team.ru/projects/maps-core-renderer-tilemill/ci/actions/launches?dir=maps/renderer/tilemill/serv) |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_renderer_tilemill_serv_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_tilemill_serv_load/) | [ core-renderer-tilemill-serv.load ](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-tilemill-serv-load-panel-main/) | [ maps_core_renderer_tilemill_serv_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_tilemill_serv_load) |
| Stable | [maps_core_renderer_tilemill_serv_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_tilemill_serv_stable/) | [ core-renderer-tilemill-serv.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-tilemill-serv-stable-panel-main/) | [ maps_core_renderer_tilemill_serv_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_tilemill_serv_stable) |
| Testing | [maps_core_renderer_tilemill_serv_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_tilemill_serv_testing/) | [ core-renderer-tilemill-serv.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-tilemill-serv-testing-panel-main/) | [ maps_core_renderer_tilemill_serv_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_tilemill_serv_testing) |

[Monitorings all (tag=a_prj_maps-core-renderer-tilemill-serv)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-renderer-tilemill-serv)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [core-renderer-tilemill-serv.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-tilemill-serv.maps.yandex.net/) | [core-renderer-tilemill-serv.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=core-renderer-tilemill-serv.maps.yandex.net;prj=core-renderer-tilemill-serv-maps;signal=service_total;) | [rtc_balancer_core-renderer-tilemill-serv_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-renderer-tilemill-serv_maps_yandex_net_sas) <br>[rtc_balancer_core-renderer-tilemill-serv_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-renderer-tilemill-serv_maps_yandex_net_vla) |
| Testing | common_default | [core-renderer-tilemill-serv.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-renderer-tilemill-serv.common.testing.maps.yandex.net"}) | [core-renderer-tilemill-serv.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-renderer-tilemill-serv_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |

### Firewall macroses

| staging | URL |
|---|---|
| Load | [ \_MAPS_CORE_RENDERER_TILEMILL_SERV_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_TILEMILL_SERV_LOAD_RTC_NETS_ ) |
| Stable | [ \_MAPS_CORE_RENDERER_TILEMILL_SERV_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_TILEMILL_SERV_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_RENDERER_TILEMILL_SERV_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_TILEMILL_SERV_TESTING_RTC_NETS_ ) |

### S3 buckets

| Staging | Settings | Dashboard |
| ------- | -------- | --------- |
| Testing | [settings](https://yc.yandex-team.ru/folders/akuhlqud6p2jumdvmipm/storage/buckets/maps-renderer-tilemill-testing) | [dashboard](https://s3-int.chv.yandex-team.ru/projects/maps-renderer-tilemill-testing/projectDashboard) |
| Stable | [settings](https://yc.yandex-team.ru/folders/akuhlqud6p2jumdvmipm/storage/buckets/maps-renderer-tilemill-stable) | [dashboard](https://s3-int.chv.yandex-team.ru/projects/maps-renderer-tilemill-stable/projectDashboard) |

## What happens when service is down

Недоступны некоторые датасеты Картографа.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/renderer-tilemill-serv/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | ```SELECT * FROM hahn.`logs/maps-log/1d/2021-12-01` WHERE vhost LIKE 'core-renderer-tilemill-serv.maps.yandex.net' limit 1;``` |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

- [продуктовое описание сервиса](https://wiki.yandex-team.ru/users/avlasyuk/map-tiling-service/)
- [описание API](docs/api.md)
- [описание архитектуры](docs/serv.md)

## Known clients

- [renderer-cartograph](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/cartograph/README.md)

## Persistent Volumes

- /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/renderer-tilemill-serv - кэш тайлсетов, для быстрого холодного старта сервиса
- /logs - логи, сюда ставится симлинка из /var/log

## Regression tests

| Имя теста | Тикет | Запустить нагрузочный тест | Lunapark |
| --------- | ----- | -------------------------- | -------- |
| rps_test | [MAPSRENDER-3102](https://st.yandex-team.ru/MAPSRENDER-3102) | Кнопка запуска — [на странице SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-renderer-tilemill-serv%22%7D). Или следуйте инструкциям ниже. | [MAPSRENDER](https://lunapark.yandex-team.ru/regress/MAPSRENDER) —> `maps-core-renderer-tilemill-serv rps_test` |

Sandbox-шедулер: [Общий шедулер регрессионных нагрузочных тестов](https://sandbox.yandex-team.ru/scheduler/702021)

Провести нагрузочный тест вручную:

+ воспользуйтесь кнопкой `Запустить` на [странице сервиса в SEDEM_SERVICE_PAGE в Sandbox](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22core-renderer-tilemill-serv%22%7D).
+ или возьмите [шаблон](https://sandbox.yandex-team.ru/template/MAPS_CORE_COMMON_LOAD_TESTING_TEMPLATE/view) —> нажмите `Create new task` —> наберите имя sedem-сервиса, уберите галочку «Run for all tests in service», наберите имя теста.
