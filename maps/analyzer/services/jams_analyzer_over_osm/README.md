# core jams analyzer over osm

Получает gps-сигналы от диспатчера анализатора пробок и строит на их основе пробки поверх данных Open Street Map.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Истомин (jemdo@yandex-team.ru) <br> Александр Ручкин (voidex@yandex-team.ru) |
| Отвественные SRE | Алексей Истомин (jemdo@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-analyzer-over-osm/ |
| CI - Покоммитный | https://a.yandex-team.ru/projects/maps-core-jams-analyzer-over-osm/ci/actions/launches?dir=maps%2Fanalyzer%2Fservices%2Fjams_analyzer_over_osm&id=build |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_jams_analyzer_over_osm_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/) | [ core-jams-analyzer-over-osm.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-stable-panel-main/) | [ maps_core_jams_analyzer_over_osm_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_over_osm_stable) |
| Prestable | [maps_core_jams_analyzer_over_osm_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_prestable/) | [ core-jams-analyzer-over-osm.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-prestable-panel-main/) | [ maps_core_jams_analyzer_over_osm_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_over_osm_prestable) |
| Testing | [maps_core_jams_analyzer_over_osm_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_testing/) | [ core-jams-analyzer-over-osm.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-testing-panel-main/) | [ maps_core_jams_analyzer_over_osm_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_over_osm_testing) |
| Load | [maps_core_jams_analyzer_over_osm_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_load/) | [ core-jams-analyzer-over-osm.load ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-load-panel-main/) | [ maps_core_jams_analyzer_over_osm_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_over_osm_load) |
| Unstable | [maps_core_jams_analyzer_over_osm_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_unstable/) | [ core-jams-analyzer-over-osm.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-unstable-panel-main/) | [ maps_core_jams_analyzer_over_osm_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_over_osm_unstable)
[Monitorings all (tag=a_prj_maps-core-jams-analyzer-over-osm)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-jams-analyzer-over-osm) |

### Balancers

| Staging | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | -------------- | -------------- | ----------------------- |
| -- |

## What happens when service is down

- Пробочные данные для автомобильной маршрутизации поверх OSM устаревают: ухудшается качество маршрутизации.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare services | /var/log/yandex/maps/analyzer-\*/* |
| Jmas uploader | /var/log/yandex/maps/tools/jams/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Hooks | Ecstatic:<br>/var/log/reload_data.log<br>/var/log/try_to_restart.log<br><br>Yacare:<br>/var/log/pre_stop.log |
| YT (access) | [YQL query](https://yql.yandex-team.ru/Operations/Yh9AFa5OD3u9SglXEBOQFTkJDz-kBuJb9F2wiLlUGIA=)<br> ```USE hahn; SELECT * FROM `logs/maps-log/1d/2022-03-01` WHERE tskv_format = 'analyzer-over-osm';``` |
| YT (signals) | [YQL query](https://yql.yandex-team.ru/Operations/Yh9mbFZ1O_jZs_nW4Qy8JtK0C7fNcnV9FIQo6H6mwRk=) |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

### Проблемы с загрузкой пробок
Мониторинги:
- Общее состояние системы:
    - [jams-upload-status](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=jams-upload-status)
- Тайминги выгрузки пробочных данных:
    - [get-jams-timings](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=get-jams-timings)

Смотреть в лог:
- `/var/log/yandex/maps/jams/tools/edge-speeds-uploader.log` для `yandex-maps-jams-speeds-osm` (основной датасет, данные берутся из segmentshandler'а)

В логе должны быть строки:

1. `Downloading from http://localhost/router_jams` - выгрузка пробочных данных, нормальное время работы 3-4 секунды, не более.
Линейно зависит от [кол-ва сегментов](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-stable-panel-main/-/12/) в памяти segmentshandler'а.

    Код ответ должен быть 200, а не 204 - это значит, что данных по сегментам в памяти недостаточно, т.е. побился стейт.
Причину смотреть в логах segmentshandler'а: `/var/log/yandex/maps/analyzer-segmentshandler/analyzer-segmentshandler.log`, искать по слову "state".

    Код ответа 5xx означает, что сервис рестартует (в норме не более 20-30 секунд на взлет), причиной могут быть как штатные перезагрузки, так и падения,
опять же см. логи сервиса.

2. `/usr/lib/yandex/maps/jams/tools/inspect_jams /dev/shm/tmp2IVc7n/edge-speeds.pb --timestamp` - проверка целостности файла с пробками

3. Синк между репликами шарда:
    ```
    coordination data: {'size': 385654, 'size_with_manoeuvres': 385654, 'last_signal_time': 1646828274}
    associates data: [{'size': 381334, 'size_with_manoeuvres': 381334, 'last_signal_time': 1646828274}, {'size': 386274, 'size_with_manoeuvres': 386274, 'last_signal_time': 1646828274}]
    ```
<br>
    В норме кол-ва сегментов ("size") не должны отличаться на порядок, иначе это значит, что одна из реплик потеряла стейт и нагоняет.
<br>
    В целом, не является проблемой, пока хотя бы одна реплика в шарде имеет достаточное кол-во сигналов (порядка 500к днем и порядка 200к ночью).
    Причину потери стейта стоит смотреть в тех же логах segmentshandler'а, если идет выкладка софта - её лучше приостановить.

4. `ecstatic upload yandex-maps-jams-speeds-osm:1of2=2022.02.17.10.26.30` - последний этап, загрузка датасета в экстатик, в норме не более 15-20 секунд.

    Загрузка может падать только в одном случае (это штатное поведение) - с сообщением
`Another version of yandex-maps-jams-speeds:1of2=2022.02.17.10.43.00 has already been published`, что всего лишь означает, что другая реплика шарда
оказалась быстрее.

### Проблемы с пересылкой данных между модулями
#### Ошибки при отправке запросов:
- [usershandler-target-error](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=usershandler-target-error)

#### Недоступность получателя:

Получатель (у usershandler'а это segmentshandler) может находиться в нескольких состояниях:
1. `online` - все ноды шарда доступны (отвечают на пинги/запросы)
2. `partially-offline` - недоступна одна нода шарда (пятисотит на пинги/запросы, либо вообще пинги/запросы не проходят)
3. `offline` - недоступно 2 и более нод
4. `unreachable` - весь шард недоступен из-за сетевых ошибок (используется не для мониторингов получателей, а для определения проблем на источнике, в случае обнаружения которых он перестаёт поджигать мониторинги недоступности получателей)

Логируются смены состояния шардов-получателей. Определить, когда с каким получателем что случилось можно, грепнув в логе `cat /var/log/yandex/maps/analyzer-*/analyzer-*.log | grep 'become'`. Получатели нумеруются с 0 (хотя сами хосты с 1).
Статистику по запросам к получателю также можно найти в логах источника по `node statistics for` и/или по имени хоста-получателя.

Мониторинги недоступности получателей:
* Частичная (только WARN):
    - [usershandler-target-partially-offline](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=usershandler-target-partially-offline)
* Критическая (2 ноды из 3-х в шарде):
    - [usershandler-target-offline](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=usershandler-target-offline)

#### Переполнение очереди на отправку:
- [usershandler-send-queue-full](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=usershandler-send-queue-full)

#### Полезные графики для оценки ситуации:
- [usershandler transmitting RPS](https://yasm.yandex-team.ru/template/panel/maps-core-jams-analyzer-over-osm-stable-panel-main/-/9/)

Причину ошибок стоит искать на получателе, вычислить его можно по логам сервиса: см. "warning"/"err" сообщения.

### Переполнение очереди задач
Мониторинги:
- [usershandler-tasks-age](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=usershandler-tasks-age)
- [segmentshandler-tasks-age](https://juggler.yandex-team.ru/check_details/?host=maps_core_jams_analyzer_over_osm_stable&service=segmentshandler-tasks-age)

Нормальными являются кратковременные всплески в моменты редеплоя, характерны для segmentshandler'а.
Стабильное превышение порога скорее всего означает, что кластер не справляется с нагрузкой.


## Documentation

### Краткое архитектурное описание

Сервис реализован в виде набора yacare-сервисов в одном контейнере:
- [analyzer-usershandler](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/usershandler)
- [analyzer-segmentshandler](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/segmentshandler)

Схема взаимодействия выглядит так (некоторые горизонтальные связи опущены для наглядности):
```
        |                 |                |
        V                 V                V
  ______________   ______________   ______________
 |              | |              | |              |
 |   external   | |   external   | |   external   |
 |  dispatcher  | |  dispatcher  | |  dispatcher  |
 |______________| |______________| |______________|
        | | |______________________________
        | |_______________                 |
        v                 v                v
  ______________   ______________   ______________
 |              | |              | |              |
 | usershandler | | usershandler | | usershandler |
 |______________| |______________| |______________|
         | | |
         | | |
         | | |
         | | |_____________________________
         | |______________                 |
         v                v                v
  ______________   ______________   ______________
 |              | |              | |              |
 | segmentshdlr | | segmentshdlr | | segmentshdlr |
 |______________| |______________| |______________|
```

Для достижения нужного уровня производительности кластер разбит на шарды, каждый из которых отвечает только за свою часть работы,
при этом для обеспечения отказоустойчивости каждый шард представлен в 3-х ДЦ.

Траффик (в виде обработанных gps-сигналов с диспатчера анализатора) льется на все реплики нужного шарда usershandler'ов: `hash(clid, uuid) % n`.

Каждая реплика поддерживает одно и то же состояние в памяти, занимается привязкой треков к графу и накапливает информацию
о скоростях проезда транспортных средств по ребрам и их сегментам. Информация о скоростях движения по сегментам ребер
периодически сбрасываются на segmentshandler'ы, разбитые на шарды по хэшу от id ребра.

Segmentshandler'ы накапливают стейт для ребер, за которые они отвечают, и периодически пересчитывают средневзвешенную
скорость проезда на сегментах. Раз в 30 секунд информация о скоростях выгружается в виде
[датасета](http://ecstatic.maps.yandex.net/pkg/yandex-maps-jams-speeds-osm/versions) в экстатик, для каждого
шарда используется свой тэг в датасете. Объединяются датасеты уже на клиентах.

### Реализация шардирования

Схема шардирования статическая и зашита в `*-hosts.*` конфигах usershandler'а.
Для корректной работы сервиса включена [move-репликация](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/replication_policies) с сохранением fqdn при замене хоста.
Т.о. при переезде пода и одной железки на другую у него не меняется fqdn, но меняется ip-адрес, из-за этого сервис, который опирается на днс,
может некоторое время пытаться ходить по старому адресу. Обычно отставание днс длится около пары минут, что гораздо меньше, чем наливка данных в новый контейнер.

### Как изменить число шардов (решардирование)
[Инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/docs/resharding.md)

### Особенности настроек сервиса в няне

0. У сервиса включена [move-репликация](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/replication_policies), это **обязательное** условие для корректной работы сервиса,
см. выше про шардирование.

1. Т.к. segmentshandler - stateful-сервисы, которые хранят состояние в памяти, то для случаев, когда необходим рестарт
(обновление софта или данных), предусмотрен механизм дампа состояния на диск (в персистентный вольюм). Полный дамп памяти на диск
не укладывается в стандартные 30 секунд, отведенные на остановку контейнера, поэтому в няне для надежности используется
кастомный pre-stop скрипт (лежит в докер-образе) и подкручены таймауты:
    - [Contaner pre stop handler](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/instance_spec)
    - [ISS3 hooks time limits -> iss_hook_stop](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/instances).
При необходимости можно их подкрутить (таймауты задаются **по обеим ссылкам**) - сейчас хватает минуты.

2. Наличие сразу нескольких сервисов в контейнере потребовало также кастомный check-скрипт, с помощью которого няня
определяет, что инстанс взлетел после деплоя (тоже лежит в докер-образе):
[How to check container readiness](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/instance_spec)

3. Дефолтная схема выкадки сервиса в няне с фиксированным окном (например, одновременно рестартуют 10% мощностей
сервиса, как только один контейнер поднялся, тут же выключается еще один старый и так далее, пока все контейнеры
не переподнимутся) не подходит для нашего шардированного сервиса, т.к. либо окно нужно брать меньше размера одного шарда (1 или
2 инстанса) - долгий деплой, либо есть риск потерять сразу целый шард на время редеплоя (нет гарантии, какие инстансы
выбираются для редеплоя). Поэтому используется [кастомный рецепт выкладки](https://nanny.yandex-team.ru/ui/#/alemate/recipes/activate_only_maps_core_jams_analyzer_per_dc.yaml/),
гарантированно работающий за раз с одним датацентром. [Параметры рецепта](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_over_osm_stable/recipes)
подобраны так, что за раз отправляется в редеплой целый ДЦ, но остановка хостов происходит последовательно с некоторым интервалом, чтобы
балансер успел отреагировать.

### Как собрать докер-образ локально
0. Настроить докер на машине, где будет производиться сборка (например, по [этой интрукции](https://wiki.yandex-team.ru/users/vmazaev/docker-v-QYP/))
1. Из директории с докер-образом выполнить: `ya package pkg.json --docker --docker-push --docker-repository maps [--custom-version <version-name>]`

## Known clients
Большинством клиентов являются потребители датасета `yandex-maps-jams-speeds-osm`
- Кластер автомобильной маршрутизации поверх OSM
    - [maps_core_driving_router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/osm/README.md)
    - [maps_core_driving_driver](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/driver/osm/README.md) - часть инфраструктуры роутеров

Источником сигналов является:
- Диспатчер основного анализатора [maps_core_jams_analyzer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/README.md)

## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-coverage5-trf](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-trf/versions) | [yandex-maps-coverage5-trf](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-trf/versions) |
| [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-geobase-tzdata](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) | [yandex-maps-geobase-tzdata](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geobase-tzdata/versions) |
| [yandex-maps-graph-osm-activator](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) | [yandex-maps-graph-osm-activator](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) |

## SLA
[Datalens](https://datalens.yandex-team.ru/hckadjiuwrf8a-maps-sla-dashboard?title=maps_core_jams_analyzer_over_osm) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_analyzer_over_osm.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/lib/yandex/maps/analyzer/states - локация для хранения стейтов segmentshandler'а между рестартами
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_TESTING_RTC_NETS_ ) |
| load | [ \_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_ANALYZER_OVER_OSM_LOAD_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: [maps-core-jams-analyzer-over-osm](https://lunapark.yandex-team.ru/regress/MAPSJAMS?service=analyzer-over-osm)
    * Sandbox:
        - [Jams Analyzer usershandler imbalance](https://sandbox.yandex-team.ru/scheduler/704927)
        - [Jams Analyzer usershandler timings](https://sandbox.yandex-team.ru/scheduler/704928)
        - [Jams Analyzer segmentshandler imbalance](https://sandbox.yandex-team.ru/scheduler/704929)
        - [Jams Analyzer segmentshandler timings](https://sandbox.yandex-team.ru/scheduler/704930)
        - [Jams Analyzer mix imbalance](https://sandbox.yandex-team.ru/scheduler/704931)
    * Тикет: https://st.yandex-team.ru/MAPSJAMS-4202

В unstable окружение сигналы из тестинга зеркалируются примерно в том же количестве, что и максимальный RPS, который получается из imbalance стрельб по диспатчеру. За это отвечает параметр `mirroring_rate`. Если в какой-то момент unstable перестанет выдерживать такой RPS, то параметр `mirroring_rate` следует уменьшить, перед этим выяснив причину просадки производительности. Если вам хочется проверить новый код в unstable на маленьком числе запросов, то вы можете временно уменьшить `mirroring_rate`.
