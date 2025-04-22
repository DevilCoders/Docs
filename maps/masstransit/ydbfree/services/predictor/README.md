# Core Masstransit Predictor

Сервис принимает GPS-сигналы общественного транспорта по хендлеру `/accept_batch` и предсказывает его движение. Прогнозы времени проезда по траектории и прибытия на остановки загружаются в ecstatic. Клиентом прогнозов является сервис [Mtinfo][mtinfo].

Источники GPS-сигналов:
* [maps-core-jams-analyzer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer)

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin), [Сергей Кузнецов](https://staff.yandex-team.ru/kuzns) |
| Исходники | [maps/masstransit/ydbfree/services/predictor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/ydbfree/services/predictor) |
| Сервис в ABC | [maps-core-masstransit-predictor](https://abc.yandex-team.ru/services/maps-core-masstransit-predictor/)|
| Проект в CI | [maps-core-masstransit-predictor](https://a.yandex-team.ru/projects/maps-core-masstransit-predictor/ci/actions/launches?dir=maps/masstransit/ydbfree/services/predictor/)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_masstransit_predictor_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_stable/) | [ core-masstransit-predictor.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-stable-panel-main/) | [ maps_core_masstransit_predictor_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_stable) |
| Prestable | [maps_core_masstransit_predictor_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_prestable/) | [ core-masstransit-predictor.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-prestable-panel-main/) | [ maps_core_masstransit_predictor_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_prestable) |
| Testing | [maps_core_masstransit_predictor_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_testing/) | [ core-masstransit-predictor.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-testing-panel-main/) | [ maps_core_masstransit_predictor_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_testing) |
| Datatesting | [maps_core_masstransit_predictor_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_datatesting/) | [ core-masstransit-predictor.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-datatesting-panel-main/) | [ maps_core_masstransit_predictor_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_datatesting) |
| Load | [maps_core_masstransit_predictor_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_load/) | [ core-masstransit-predictor.load ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-load-panel-main/) | [ maps_core_masstransit_predictor_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_load) |
| Unstable | [maps_core_masstransit_predictor_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_predictor_unstable/) | [ core-masstransit-predictor.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-unstable-panel-main/) | [ maps_core_masstransit_predictor_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_predictor_unstable) |


[Monitorings all (tag=a_prj_maps-core-masstransit-predictor)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-masstransit-predictor)


## What happens when service is down

[Mtinfo][mtinfo] перестают получать свежие прогнозы и траекторию движения транспорта; они устаревают, а потом пропадают.

## Logs
Логи Supervisord и stderr\stdout подконтрольных ему процессов лежат в /var/log/supervisor/*

Логи, управляемые unified_agent:
- **predictor** - yacare-сервант
- **predictions** - предсказания, выгружаемые в Logbroker
- **nginx** - access-логи nginx
- **nginx_error** - error-логи nginx
- **ecstatic**

Посмотреть имена всех логов unified: ```unified_agent select -l```

Прочитать конкретный лог: ```unified_agent select -s <storage> (-f)```

[подробно про unified_agent select](https://docs.yandex-team.ru/unified_agent/operations/#select-command)

Access-логи в YT: https://yql.yandex-team.ru : ``SELECT * FROM hahn.`logs/maps-log/1d/2021-04-20` WHERE vhost LIKE '%core-masstransit-predictor%';``


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

### Если предсказаний нет
Проверяем в `ecstatic` какие шарды отсутствуют.

1. Смотрим в логи `uploader`: `/var/log/user.log`.
На некоторых хостах могут присутствовать записи вида `Failed to run ecstatic upload` – это ок, т.к. все реплики шарда пытаются загрузить одну версию датасета параллельно, но удается это только одной из них.
2. Если проблема в `ecstatic`, смотрим туда. Если проблема в сервисе, смотрим в логи `/var/log/yandex/maps/predictor/*` в поисках записей `GET /export`.

### Если предсказаний мало
1. Проверяем наличие всех шардов в датасете (задаются посредством тэгов), см. предыдущий пункт.
2. Смотрим на метрику количества имеющихся прогнозов (например, [stable](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-stable-panel-main/-/11/))
3. Смотрим на метрику отфильтрованных `clid` (например, [stable](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-stable-panel-main/-/9/)). Эта фильтрация задается конфигом партнеров (для `stable` это `/var/lib/yandex/maps/ecstatic/preserved_data/yandex-maps-masstransit-regions-config-production/masstransit-regions.conf`)
4. Смотрим на метрику устаревших сигналов (например, [stable](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-predictor-stable-panel-main/-/10/))

### Если загорелся мониторинг на `crash`
Нужно убедиться, что это не push-client: `dmesg -T | grep segfault`. Если это он, то проигнорировать этот crash.

## Documentation

Описание архитектуры: https://st.yandex-team.ru/MAPSJAMS-3386

Сервис разделен на шарды, содержащие равные реплики.
Конфигурация шардирования задается через [конфиг Dispatcher](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/dispatcher/config), также см. [aliases](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/common/url_resolver/aliases.default.json).

Выгрузка предсказний происходит посредством ручки `/export`.

Сервис загружает готовые предсказания в `Logbroker` в [аккаунт maps-masstransit-predictor](https://logbroker.yandex-team.ru/logbroker/accounts/maps-masstransit-predictor) посредством `push-client`. Файлы с предсказаниями: `/var/log/yandex/maps/predictor/predictions/*`.

У сервиса отсутствует стейт, поэтому после старта какое-то время (60 сек) предсказания не загружаются в экстатик. Некоторые автобусы присылают свои GPS-сигналы реже чем раз в минуту, поэтому после рестарта может __не быть__ предсказаний для таких автобусов.

### Выгружаемые датасеты
| Name | URL/path |
|---|---|
| stable | http://ecstatic.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions |
| testing | http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions |
| datatesting | http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions |
| unstable | http://core-ecstatic-coordinator.common.unstable.maps.yandex.net/pkg/yandex-maps-masstransit-predictions/versions |

## Known clients
* [Mtinfo][mtinfo]

## SLA

[TODO Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[TODO Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_MASSTRANSIT_PREDICTOR_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PREDICTOR_STABLE_RTC_NETS_ ) |
| datatesting | [ \_MAPS_CORE_MASSTRANSIT_PREDICTOR_DATATESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PREDICTOR_DATATESTING_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_MASSTRANSIT_PREDICTOR_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PREDICTOR_TESTING_RTC_NETS_ ) |
| load | [ \_MAPS_CORE_MASSTRANSIT_PREDICTOR_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PREDICTOR_LOAD_RTC_NETS_ ) |
| unstable | [ \_MAPS_CORE_MASSTRANSIT_PREDICTOR_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PREDICTOR_UNSTABLE_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSJAMS?service=predictor
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/519015


<!-- links -->
[mtinfo]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/mtinfo
