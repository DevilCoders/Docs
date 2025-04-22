# Core Masstransit Realtime Receiving

Доставка realtime данных общественного транспорта в [maps-core-masstransit-predictor](https://abc.yandex-team.ru/services/maps-core-masstransit-predictor/). Ходит за данными к поставщикам и пересылает их в [jams-analyzer](https://abc.yandex-team.ru/services/maps-core-jams-analyzer/)

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin), [Андрей Козлов](https://staff.yandex-team.ru/pedeathtrian) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/realtime_receiving |
| Сервис в ABC | [maps-core-masstransit-realtime-receiving](https://abc.yandex-team.ru/services/maps-core-masstransit-realtime-receiving/) |
| Проект в CI | [maps-core-masstransit-realtime-receiving](https://a.yandex-team.ru/projects/maps-core-masstransit-realtime-receiving/ci/actions/launches?dir=maps/masstransit/info/realtime_receiving) |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_masstransit_realtime_receiving_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_stable/) | [ core-masstransit-realtime-receiving.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-realtime-receiving-stable-panel-main/) | [ maps_core_masstransit_realtime_receiving_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_realtime_receiving_stable) |
| Prestable | [maps_core_masstransit_realtime_receiving_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_prestable/) | [ core-masstransit-realtime-receiving.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-realtime-receiving-prestable-panel-main/) | [ maps_core_masstransit_realtime_receiving_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_realtime_receiving_prestable) |
| Datavalidation | [maps_core_masstransit_realtime_receiving_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_datavalidation/) | [ core-masstransit-realtime-receiving.datavalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-realtime-receiving-datavalidation-panel-main/) | [ maps_core_masstransit_realtime_receiving_datavalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_realtime_receiving_datavalidation) |
| Datatestingvalidation | [maps_core_masstransit_realtime_receiving_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_datatestingvalidation/) | [ core-masstransit-realtime-receiving.datatestingvalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-realtime-receiving-datatestingvalidation-panel-main/) | [ maps_core_masstransit_realtime_receiving_datatestingvalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_realtime_receiving_datatestingvalidation) |
| Testing | [maps_core_masstransit_realtime_receiving_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_testing/) | [ core-masstransit-realtime-receiving.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-realtime-receiving-testing-panel-main/) | [ maps_core_masstransit_realtime_receiving_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_realtime_receiving_testing) |
[Monitorings all (tag=a_prj_maps-core-masstransit-realtime-receiving)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-masstransit-realtime-receiving)


## What happens when service is down

Пропадут метки общественного транспорта и прогонозы прибытия в некоторых городах.
На момент написания - в Москве и Санкт-Петербурге. Актуальный список - в конфиге.

## Logs
| Name | URL/path |
|---|---|
| Service | `/var/log/yandex/maps/realtime_receiving/*` |
| Ecstatic | `/var/log/yandex/maps/ecstatic-agent/*` |
| Supervisord | `/var/log/supervisor/*` |
| Syslog (unfiltered) | `/var/log/syslog` |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

* **Горит мониторинг `{clid}-lock-was-not-acquired`**:\
    См. https://wiki.yandex-team.ru/maps/dev/core/masstransit/rfc/gps-fetch/#sinxronizacija\
    Мониторинг загорается, если каждый инстанс сообщил, что лок взять не удалось.

    **Что делать**:\
    Посмотреть в логах любой из машинок, почему не удаётся взять лок.

    Если выкатились новые данные, и сервис не может их прочитать, то откатить данные на рабочую версию здесь:\
    https://garden.maps.yandex-team.ru/merge_masstransit_for_realtime_deployment\
    Чтобы откатить данные для clid из [`clids_with_rapid_data`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/realtime_receiving/docker/install/etc/template_generator/config.d/10-setup.yaml#L12), можно удалить последний Sandbox ресурс [`MAPS_MASSTRANSIT_VEHICLE_TASKS_RESOURCE`](https://sandbox.yandex-team.ru/resources?type=MAPS_MASSTRANSIT_VEHICLE_TASKS_RESOURCE) в нужном окружении. Для ускорения процесса можно дополнительно сделать `supervisorctl restart moscow_data_updater` на машинках.

* **Горит мониторинг `{clid}-active-workers-count`**:\
    Мониторинг загорается, если один или несколько инстансов работает автономно, без взятия лока.\
    Такое должно случаться только если машинка не смогла достучаться до Locke чтобы проверить состояние лока.

    **Что делать**:\
    Посмотреть логи сервиса с нужным clid. В них должна быть причина, почему машинка не смогла достучаться до кластера.\
    Проверить состояние https://locke.yt.yandex-team.ru\
    Если планируется долгий downtime, а mtpredictor-у плохеет из-за нагрузки, то попробовать отключить часть ДЦ через [ITS](https://nanny.yandex-team.ru/ui/#/its/locations/maps/man/backend_detach/).

* **Горит мониторинг `fetch-realtime-fails`**:\
    Это общий мониторинг, который загорается, если хотя бы для одного clid мы получаем ответ не 200 при скачивании данных.

    **Что делать**:\
    Выяснить, с каким clid возникли проблемы, посмотрев на графики "Fetch realtime http codes" на sedem панели.\
    Посмотреть логи сервиса с нужным clid и найти код ответа и описание. Если код не стандартный, то найти значение можно [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/library/http/fetch/exthttpcodes.h?rev=r3342757).\
    Если проблема возникла с clid `moscow`, см. [maps_core_masstransit_partners_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/partners_proxy).

* **Горит мониторинг `{clid}-static-data-age`**:\
    Загорается для clid, статику для которых мы скачиваем из Sandbox напрямую с машинок.

    **Что делать**:\
    Посмотреть состояние и логи последних задач [Sandbox scheduler-а](https://wiki.yandex-team.ru/maps/dev/core/masstransit/sandbox_schedulers/#mapsmasstransitimportvehicletasks).\
    Если свежие ресурсы в sandbox есть, то посмотреть логи data_updater-а и `{clid}.log` в папке с логами сервиса (см. выше).\
    Если сервис не может прочитать свежие данные, потому что они некорректные, то сообщить об этом поставщику.\
    `moscow/TSmgt.json`, `moscow/TScomp.json` - ЦОДД;\
    `moscow/ROUTES`, `moscow/VEHICLE_TASK` - МГТ;\
    `moscow/gkuop.csv` - ГКУ Организатор Перевозок.

## Documentation

https://st.yandex-team.ru/MTDEV-657\
https://wiki.yandex-team.ru/maps/dev/core/masstransit/rfc/gps-fetch/

### Чеклист добавления нового города
* Написать класс-наследник `DataManager`
* Добавить поддержку нового clid в функции `spawnDataManager` и `getYasmPort` в `bin/main.cpp`
* Добавить clid и порт в [конфиге template_generator](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/realtime_receiving/docker/install/etc/template_generator/config.d/10-setup.yaml#L12)
* Добавить yasm ручку с новым портом в каждый няня-сервис во вкладке Instance Spec -> YASM unistat endpoints


## Known clients
Клиентов не должно быть, это внутренний сервис для доставки данных

## Ecstatic Datasets
| Stable | Testing | Datatesting |
| ------ | ------- | ------- |
| [yandex-maps-masstransit-data-for-realtime](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-data-for-realtime/versions) | [yandex-maps-masstransit-data-for-realtime](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-data-for-realtime/versions) | [yandex-maps-masstransit-data-for-realtime](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-data-for-realtime/versions) |


## Persistent Volumes
* `/logs` - логи, сюда ставится симлинка из /var/log
* `/var/lib/yandex/maps` - раздел со статическими данными

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_stable/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_prestable/yp_pods/ |
| Datavalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_datavalidation/yp_pods/ |
| Datatestingvalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_datatestingvalidation/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_realtime_receiving_testing/yp_pods/ |
## Firewall macros
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_MASSTRANSIT_REALTIME_RECEIVING_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_REALTIME_RECEIVING_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_MASSTRANSIT_REALTIME_RECEIVING_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_REALTIME_RECEIVING_TESTING_RTC_NETS_ ) |
