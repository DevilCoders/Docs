User Edits Metrics
==================
User Edits Metrics is a service that calculates metrics for [edits processing][edits processing tab] and [deployment][deployment tab] tabs of [NMAPS dashboard][dashboard]. This dashboard uses data from the following reports populated by this tool:
- [User Edits Processing Times][User Edits Processing Times];
- [Consolidated Deployment Time][Consolidated Deployment Time]; and
- [Deployment SLA][Deployment SLA].


How-to Add a Metric
-------------------
*Note*. This document describes how to add a metric for an event from [`publication_check_worker/lib/branch_events.h`][branch_events.h].

The metric can be added by performing the following steps:
1. Update the following objects with this new event in [`util.h`][util.h] and [`util.cpp`][util.cpp]:
   - `Event` enum and its representation `EVENT_REPRESENTATION`;
   - `BRANCH_BASE_EVENTS` set;
   - `DEPLOYED_TO_PRODUCTION_EVENTS` set (see a note below, for more information); and
   - `EVENT_TO_BROKEN_SLA_EVENT` and `EVENT_TO_REAL_SLA_EVENT` maps.
2. Add this new event to [`metrics_calculator.cpp`][metrics_calculator.cpp]:
   - `DeploymentType` enum; and
   - `EventToDeploymentType` map.
3. Add new measures to `UserEditsProcessingTimesMeasures` and `DeploymentSlaMeasures` structures from [`user_edits_processing_times.h`][user_edits_processing_times.h] and  [`deployment_sla.h`][deployment_sla.h]. Processing of these new measures must be added to `add()`, `keyValues()`, `print()` and `printHeader()` methods.
4. Add new measures to [User Edits Processing Times][User Edits Processing Times] and [Deployment SLA][Deployment SLA] reports (using [migrations][migrations] for [Stat db][Stat db]).

*Note*. Metrics added to `DEPLOYED_TO_PRODUCTION_EVENTS` could temporary break *Broken SLA (Total)* and *Real SLA (Total)* graphs because these graphs represent window functions calculated from these metrics. Broken graphs will be restored when sufficient number of measures are accumulated. However, to keep graphs functional it is recommended not to add events to `DEPLOYED_TO_PRODUCTION_EVENTS` set prior to the moment when all needed measures are accumulated.


Dry Run Mode
------------
This tool can be run in a kind of 'dry run' mode by executing it with `--no-upload` and `--dump-dir` options.


Notes About Reports
-------------------
The easiest way to open a report slice corresponding to a graph on the [dashboard][dashboard] is:
1. Press button at the right top corner of the graph.
2. Choose 'Show sources' button.
3. Select the source of interest.


Usage
-----

```sh
Usage: user_edits_metrics <options...>

  --config <filename>                              Services config filename. (default: '/etc/yandex/maps/wiki/services/services.xml')
  --window <duration>                              Window duration. (default: 24h)
  --single-metric-depth <n>                        How many windows deep a single metric must be calculated starting from the first non-null value. (default: 40)
  --total-depth <n>                                How many windows deep all metrics must be calculated. (default: 60)
  --quantiles <value>                              Comma-separated list of quantiles to calculate (0 <= q <= 1). (default: 0.5,0.85,0.95)
  --dump-dir <dir>                                 Directory to dump metrics in CSV format. Do not dump by default.
  --no-upload                                      Do not upload collected data to Stat db.

'Deployment days out of SLA' (DDS) and 'Achievable SLA' metrics:
  --dds '<window> <quantile> <budget>' ...   window   Sliding window size to calculate the metric.
                                             quantile Quantile to calculate the metric.
                                             budget   Maximum number of days in the window allowed to be out of SLA.
                                             (default: '30 0.85 5', '30 0.95 5', '10 0.85 2', '10 0.95 2')
                                             This option can be repeated several times.
```


Логика вычисления метрик
------------------------

1. Считываем из базы таблицу `revision.branch`, из неё достаём значения `<branch_id, Event, region, deployed_time>`. База заполняется в [publication_check_worker][publication_check_worker].
2. На основании этих значений для каждого event-а считаем map: Event -> список регионов, где event хоть раз случился за время `options.window * opitons.totalDepth`. В список для каждого event-а добавляем все aoi регионы и `all_regions`.
3. Считаем метрики времени "от правки до продакшена", которые позже запишем в отчёт [User Edits Processing Times][User Edits Processing Times]:
    - пробегаем по всем коммитам каждого дня от "сегодня" и на `options.totalDepth` дней назад: для каждого дня считаем свой набор метрик
    - реализация в `MetricsCalculator::calculate()` из `metrics_calculator.cpp` и `quantileMetric()` из `metrics.cpp`. Выбираем все подходящие коммиты: по региону, `inTrunk` и `userType`. Сортируем их по времени публикации, из отсортированных берём нужный квантиль
    - Если нужный квантиль попал на коммит, для которого не получилось посчитать момент деплоя, то посчитать метрику не удастся
    - При вычислении метрики event-а по `all_regions` "всеми" считаем только те регионы, в которых удалось найти этот event.
    - Добавление регионов для коммита в `addCommitData` в `commit_loader.cpp`.
    - *Примечание*. В `all_regions` попадают коммиты из всех регионов, даже если event происходит не во всех. Время деплоя event-а в `all_regions` считаем так: берём времена event-а для коммита по всем регионам, куда попал коммит, выбираем минимальное время.
4. Считаем метрики SLA (опция `dds`). Для дефолтного значения `30 0.85 5` получим следующее:
    - При вычислении метрик для коммитов из транка используем `sla=5`, для коммитов не из транка - `sla=1`. `sla=5` означает требование, чтобы данные от правки доезжали до продакшена за 5 дней
    - `window=30`: считаем за сколько доезжают правки на протяжении 30 дней.
    - `quantile=85`: выбираем посчитанные ранее метрики с этим квантилем.
    - `budget=5`: разрешаем, чтобы в течение времени `window=30` дней `sla` нарушалось `budget=5` раз.
5. Для каждого дня считаем, за какое время нужный процент правок добирается до продакшена, реализация в `getConsolidatedDeployedMetricsWithEstimations`. Данные публикуем в отчёт [Consolidated Deployment Time][Consolidated Deployment Time]. Из всех метрик, посчитанных в какой-то день, выбираем максимум. Если в какой-то день опубликованы не все данные, то метрику посчитать не получается. Если какую-то метрику не удалось посчиталась, то для неё в `addEstimatedMissingMetrics` считаем оценку. Для этих вычислений из опций dds нужен только квантиль.
6. Вычисляем метрики в отдельности каждому event-у, позже публикуем их в отчёт [Deployment SLA][Deployment SLA].
    - для каждого event-а вычисляем:
        * `real_sla` - какой должен быть sla, чтобы он нарушался не более `budget` дней в окне `window`. Реализация в `achievableSlaInSlidingWindow()`
        * `broken_sla` - количество дней за период `window`, когда `sla` нарушался. Реализация в `daysOutOfSlaInSlidingWindow`


*Примечание*. Сейчас в любой отчёт данные публикуются csv-файлом. Любые данные в этом файле затирают данные из отчёта для соответствующих dimensions. В частности, в csv пустые значения для каких-то `measures` затирают записанные в отчёте непустые значения.


Логика формирования задачи в Трекере
--------------------------------------

Цель формирования задачи в Трекере - предупредить заранее о приближающихся или прогрессирующих проблемах с SLA.
Настройки уведомлений настраиваются в [st_notifier.cpp][st_notifier.cpp] в структуре `NotifySettings`.
Идея заключается в том, чтобы заинтересованным лицам, указанным в поле `followers`, пришло уведомление о создании в
очереди `queueKey` задачи с комментарием. В комментариях к задаче будет отслеживаться:
- динамика увеличения обобщенной (total) метрики `broken_sla`, если она превысила некоторое пороговое значение
  `slaWarningLevel`;
- какие конкретно модули вызвали увеличение `broken_sla`.

**Алгоритм создания/обновления задачи:**

1. На основании описанной выше логики вычисления метрик, рассчитываем `broken_sla` для деплоев всех модулей,
   при заданных настройках `NotifySettings`. И получаем обобщенную (total) метрику `broken_sla`.
2. Если обнаруживается, что на последний день метрик имеется достижение или превышение `slaWarningLevel`,
   то запускается процесс формирования уведомления.
    - Сначала ищется последний уже открытый тикет с заданным в `NotifySettings` названием. Если такого тикета нет,
      то он создается.
    - Далее, по наличию тэга с датой в тикете, смотрится на какое число было последнее формирование предупреждений.
      Тэг хранит дату в ISO формате: `last update by user_edits_metrics YYYY-MM-DD`.
    - Отсчитывая от этой даты исследуется обобщенная метрика `broken_sla`.
    - Если на данном отрезке времени обнаруживается момент достижения `slaWarningLevel`, то в тикете формируется
      комментарий, в котором пишется о факте достижения, а также перечисляются значения всех ненулевых `broken_sla`
      по модулям на этот день.
    - Далее для каждого дня, когда было дальнейшее увеличение обобщенной метрики `broken_sla`, в комментарий
      дописывается факт увеличения и информируется, какие именно модули в этот день спровоцировали рост `broken_sla`.
    - В конце в тикете удаляются старые тэги с датой и выставляется новый. В новом тэге будет указана дата последних
      учтенных обобщенных данных `broken_sla` (может не совпадать с датой обновления тикета).

[Consolidated Deployment Time]:  https://datalens.yandex-team.ru/datasets/8y3bqs0qvhnk0-consolidated-deployment-time
[Deployment SLA]:                https://datalens.yandex-team.ru/datasets/e49hklqigbfg6-deployment-sla
[User Edits Processing Times]:   https://datalens.yandex-team.ru/datasets/xns425xzjprap-user-edits-processing-times
[dashboard]:                     https://datalens.yandex-team.ru/bq3fxpmya6e67-kpi
[deployment tab]:                https://datalens.yandex-team.ru/bq3fxpmya6e67-kpi?tab=Nw4
[edits processing tab]:          https://datalens.yandex-team.ru/bq3fxpmya6e67-kpi?tab=kWM

[Stat db]: https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-postgresql/cluster/mdbuj2taicnnb0ff8lnb
[migrations]: https://a.yandex-team.ru/arcadia/maps/wikimap/stat/migrations

[branch_events.h]:               https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/publication_check_worker/lib/branch_events.h
[deployment_sla.h]:              https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/deployment_sla.h
[metrics_calculator.cpp]:        https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/metrics_calculator.cpp
[st_notifier.cpp]:               https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/st_notifier.cpp
[user_edits_processing_times.h]: https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/user_edits_processing_times.h
[util.cpp]:                      https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/util.cpp
[util.h]:                        https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics/lib/util.h

