# Перепартиционирование по шагам

В данной инструкции описывается как правильно сделать переразбиение на партиции для автосборки.
Сейчас партиционирование включено для [linux](https://a.yandex-team.ru/arc_vcs/autocheck/balancing_configs/autocheck-linux.json) и [sanitizers](https://a.yandex-team.ru/arc_vcs/autocheck/balancing_configs/autocheck-sanitizers.json), и данная инструкция работает для препартиционрования обоих конфигураций.

## Изменение количества партиций

* Подготовить и закоммитить PR с конфигурацией балансировки нового числа партиций
  * Сгенерировать конфигурацию балансировки партиций для нового числа партиций [Sandbox задача: BALANCING_PARTITION](https://sandbox.yandex-team.ru/template/AUTOCHECK_BALANCING_PARTITION/view)
  * Клонировать последнюю удачно отработавшую задачу [AUTOCHECK_BALANCER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=AUTOCHECK_BALANCER&created=14_days)
  * Снять галочку с параметра `Create PR (create_pr)`
  * В параметре `Autocheck partitions configurations (partitions_configs)` перечислить ресурсы с отбалансированными автосборочными конфигурациями [AUTOCHECK_BALANCING_CONFIG](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_CONFIG)
  * Опционально, если на данном этапе не хочется ждать балансировки кластеров, в параметре `Consumption statistics by autocheck configurations (stat_partitions)` указать последний доступный ресурс [AUTOCHECK_BALANCING_CONSUMPTION_STATISTICS](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_CONSUMPTION_STATISTICS)
  * В ресурсе [AUTOCHECK_BALANCING_RESULT](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_RESULT) будут конфиги с балансировкой партиций для всех автосборочных конфигураций.
  * Закоммитить новый конфиг: [balancing_configs/...](https://a.yandex-team.ru/arcadia/autocheck/balancing_configs)
* подготовить PR с изменениями количества партиций:
  * Запустить [AUTOCHECK_BALANCER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=AUTOCHECK_BALANCER&created=14_days) из предыдущего пункта обнулив параметр `stat_partitions`, из результирующего ресурса получить [autocheck.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/autocheck/autocheck.yaml)
  * обновить конфигурацию прогреватора ГГ: [sandbox/projects/devtools/YaMakeYmakeCacheHeater/autocheck_params/init.py](https://a.yandex-team.ru/arc_vcs/sandbox/projects/devtools/YaMakeYmakeCacheHeater/autocheck_params/__init__.py?rev=ac2aeeb83f49a16da62c135d7ee67b9b61d767df#L195)
  * поправить тесты [devtools/ya/build/tests/perf](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/ya/build/tests/perf/test_san_like_dist.py?rev=r8360821#L547)
  * канонизировать:
    * [sandbox/projects/devtools/YaMakeYmakeCacheHeater/autocheck_params/ut](https://a.yandex-team.ru/arc_vcs/sandbox/projects/devtools/YaMakeYmakeCacheHeater/autocheck_params/ut)
    * [devtools/ya/build/tests/perf](https://a.yandex-team.ru/arc_vcs/devtools/ya/build/tests/perf)
    * [devtools/ya/yalibrary/platform_matcher/tests](https://a.yandex-team.ru/arc_vcs/devtools/ya/yalibrary/platform_matcher/tests)

* изменить конфигурацию планировщика [YMAKE_CACHE_HEATER](https://sandbox.yandex-team.ru/scheduler/18501/view) -- это надо сделать за час до переключения и запустить прогрев вручную; убедиться, что кэши сварились и только потом переключать автосборку
* изменить конфигурацию планировщика тестов [YMAKE_CACHE_TEST](https://sandbox.yandex-team.ru/scheduler/18535/view)
* закоммитить PR с изменениями `autocheck.yaml`
* добавить график на [дашборд](https://datalens.yandex-team.ru/n4soqpr5f7mkk-ymake-dashboard?state=5d86fff4201) для нового теста

Для санитайзеров **не** надо:

* править тесты на инвалидацию кэшей -- они запускаются только для Linux, при перепартицировании Linux надо будет править эти тесты
* править тесты на мигающие UIDы -- они запускаются только для Linux, при перепартицировании Linux надо будет править такие тесты в `ya` и `ymake`.

## Перебалансировка партиций

Перебалансировка партиций выполняется автоматически Sandbox-задачей, запускаемой по расписанию.
[планировщик AUTOCHECK_BALANCER](https://sandbox.yandex-team.ru/scheduler/711782/view)
[код задачи AUTOCHECK_BALANCER](https://a.yandex-team.ru/arcadia/devtools/autocheck/partition_metod/AutocheckBalancer)
Все манипуляции происходят в trunk. Если необходимо использовать какую нибудь ревизию или ветку, то это можно указать в параметре `arcadia_url`

Для запуска необходимо указать:

* _ya_token_ - токены для arc
* _yt_token_ - токены для YT,
* _yt_pool_ - YT pool  для расчета статистики сборок top-level директорий (TLD)
* stat_collector_bin - Ресурс (тип [AUTOCHECK_BALANCING_STATISTICS_COLLECTOR](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_STATISTICS_COLLECTOR)) с собранным [кодом](https://a.yandex-team.ru/arcadia/devtools/autocheck/partition_metod/stat_collector) расчета статистики сборок top-level директорий

по умолчанию список кластеров Distbuild берется из [конфига prod_pools.json](https://a.yandex-team.ru/arcadia/devtools/distbuild/pool_config_manager/data/prod_pools.json), но другой состав можно установить в параметре `clusters`
Если необходимо, что бы конфигурация для ГрафоГенерации соответствовала конфигурации Distbuild'а, но надо выставить параметр `sync_gg_config` в True

### Алгоритм работы задачи

  1. Для всех автосборочных конфигураций на основании [конфига autocheck.yaml](https://a.yandex-team.ru/arcadia/autocheck/autocheck.yaml) у которых кол-во партиций > 1 запускается задача [BALANCING_PARTITION](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=BALANCING_PARTITION&created=14_days):
      1. Составление списка top-level директорий [src](https://a.yandex-team.ru/arc_vcs/devtools/platform_miner/miner.py?#L42).
          1. Используя мини-аркадию (только папки _autocheck_ и _build_) запускается максимальная сборка таргета autocheck с записью evlog-а. Из событий `NEvent.TInvalidRecurse` получаем top-level директории
          1. Для каждой пары платформа-TLD запускается графогенерация и из графа собираются uuid'ы
          1. Формируется ресурс типа [AUTOCHECK_BALANCING_YA_MAKE_PARSE_RESULT](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_YA_MAKE_PARSE_RESULT) в нем файл uid_collection.json со списком TLD и uuid's
      1. Распределение TLD по партициям
          1. Сортируем TLD по кол-ву uuid в обратном порядке
          1. Для linux применяем "серебряный костыль": распределяем TLD из [специального списка](https://a.yandex-team.ru/arc_vcs/devtools/autocheck/partition_metod/AutocheckBalancer/balancing_partitions.py?rev=3aa28543595086474f04571e148861c2f3fc3f9a#L12) по партициям
          1. Самую большую TLD кладем в партицию где меньше всего уникальный uuid's. Повторяем процесс до исчерпания TLD's.
      1. Формируется ресурс типа [AUTOCHECK_BALANCING_CONFIG](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_CONFIG)
  1. Расчет статистик нагрузки TLD
      1. Из логов distbuild за последние 30 дней рассчитываем суммарное кол-во затраченных slot_time на каждый TLD, далее используя конфиг балансировки партиций рассчитывается затраченные slot_time на партицию. `Можно описать хитрую модель определения ноды к тому или иному TLD`
      1. Формируется ресурс [AUTOCHECK_BALANCING_CONSUMPTION_STATISTICS](https://sandbox.yandex-team.ru/resources?type=AUTOCHECK_BALANCING_CONSUMPTION_STATISTICS) в нем находится информация о затраченных ресурсах для каждой партиции в каждой автосборочной конфигураций
  1. Балансировка кластеров
      1. На основании конфига [prod_pools.json](https://a.yandex-team.ru/arc_vcs/devtools/distbuild/pool_config_manager/data/prod_pools.json) рассчитывается доля каждого кластера в общем кол-ве доступных ресурсов
      1. Используя информацию о суммарном потреблении ресурсов за последние 30 дней рассчитывается емкость каждого кластера
      1. Все партиции для всех автосборочных конфигураций сортируются по убыванию необходимых ресурсов.
      1. Последовательно распределяются партиции по наименее нагруженным кластерам
      1. Ищутся пары, тройки, ... шестерки партиций у самого перегруженного и недогруженного кластеров, что бы привести их в лучший баланс.
      1. Вносятся изменения в [autocheck/balancing_configs/](https://a.yandex-team.ru/arc_vcs/autocheck/balancing_configs) и [autocheck/autocheck.yaml](https://a.yandex-team.ru/arc_vcs/autocheck/autocheck.yaml)
      1. Создается PR. Ссылка на PR кладется в параметр `result_pull_request`
