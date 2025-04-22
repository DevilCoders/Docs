Основные метрики склейки
========================

https://stat.yandex-team.ru/Crypta/MatchingBaseMetrics
------------------------------------------------------

v1 with @generate_date [//home/crypta/production/state/graph/dicts/matching/exact_vertices_by_key]
v2 with @generate_date [//home/crypta/production/state/graph/v2/matching/vertices_no_multi_profile_by_id_type]

### Запуск

```bash
$ ./crypta/graph/metrics/stats_base/bin/stats-base --help
usage: stats-base [-h] -s SOURCE -d DATE -v VERSION [--local]
                  [--metrics METRICS [METRICS ...]]

Calc base matching metrics on YQL

optional arguments:
  -h, --help            show this help message and exit
  -s SOURCE, --source SOURCE
                        YT path to matching source table Example: //home/crypt
                        a/production/state/graph/v2/matching/vertices_no_multi
                        _profileAllow {date} placeholder
  --history-dir HISTORY_DIR
                        Needed for id's stable metrics. YT path to directory
                        with backups of matching source table. Example:
                        //home/crypta/archive/graph/vertices_no_multi_profile
  --export-dir EXPORT_DIR YT path to directory with export crypta matching for vulture
                        Example: //home/crypta/production/state/graph/v2/export/vulture
  --debug-dir DEBUG_DIR YT path to directory where will be stored
                        artifacts of calculating retargeting metrics
                        Example: //home/crypta/production/graph/metrics
  -d DATE, --date DATE  Date for metrics calc. Allow "@generate_date" - in
                        this case date will be get from table attributes.
  -v VERSION, --version VERSION
                        Matching version
  --local               Do not upload report on YT and Statface
  --metrics METRICS [METRICS ...]
                        Space separated list of metrics to calc. Filter by
                        prefix in config/metrics.yaml (default: all metrics)
```

Параметры запуска:

flag|description|example
----|-----------|-------
-s \--source|Исходная таблица со склейкой. Доступен плейсхолдер `{date}`|`//home/crypta/production/state/graph/{date}/exact/cluster/vertices`, `//home/crypta/production/state/graph/v2/matching/vertices_no_multi_profile_by_id_type`
-d \--date|Дата для расчета метрик. Подставляется в путь к таблице. Доступна в контексте для рендера запроса.|`2018-08-28`
-v|Версия склейки (нужна для адаптеров исходной таблицы в инклюдах запроса)|`v1`, `v2`, `v2exp`
_опциональный_ \--history-dir|Папка с бекапами склейки, нужна для метрик стабильности идентификаторов.|`//home/crypta/archive/graph/vertices_no_multi_profile`
_опциональный_ \--local|Не записывать результат обсчета в YT и Statface|
_опциональный_ \--metrics {list}|Список метрик для обсчета. По умолчанию считаются все.|`radius`, `ads`, ...

Локально добавляй перед запросом ```ENV_TYPE=development```, чтобы запускать yt-операции c правами робота crypta.
Для этого предварительно надо загрузить его token в интерфейсе YQL.

Пример запуска с указанием конкретных метрик (`radius`, `ads`):

```bash
$ ENV_TYPE=development YT_POOL=crypta_graph ./crypta/graph/metrics/stats_base/bin/stats-base \
    -s //home/crypta/production/state/graph/v2/matching/vertices_no_multi_profile_by_id_type \
    -d 2018-08-23 -v v2 --local --metrics ads radius


Run YQL query (/templates/yql/radius/radius.sql)
                                          0
version                                  v2
ts                               1535025600
radius_x_similarity_intersect         52505
radius_x_similarity_union            121218
radius_x_similarity            0.4331452425
radius_x_matched_rlogins              10736
radius_x_coverage              0.8630918884
radius_x_rlogins_count                12439
radius_x_crypta_ids_count             23039
radius_x_precision_mean_opt    0.7339067151
radius_x_precision_median_opt           1.0
radius_x_recall_mean_opt       0.2539698652
radius_x_recall_median_opt     0.1903485679


Run YQL query (/templates/yql/ads/experiment.sql)
                             0
version                     v2
ts                  1535025600
ads_x_rsya_cost_d  6.747228652
```

Пример запуска без указания конкретных метрик (считает для всех из [`configs/metrics.yaml`](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/stats_base/lib/configs/metrics.yaml))

```bash
$ ENV_TYPE=development YT_POOL=crypta_graph ./crypta/graph/metrics/stats_base/bin/stats-base \
    -s //home/crypta/production/state/graph/{date}/exact/cluster/vertices \
    -d 2018-08-25 -v v1 --local


Run YQL query (crypta/graph/metrics/stats_base/yql/radius/radius.sql)
                                          0
version                                  v1
ts                               1535198400
radius_x_similarity_intersect         32538
radius_x_similarity_union            118454
radius_x_similarity            0.2746889088
radius_x_matched_rlogins               9995
radius_x_coverage              0.8056585523
radius_x_rlogins_count                12406
radius_x_crypta_ids_count             14101
radius_x_precision_mean_opt    0.8371278605
radius_x_precision_median_opt           1.0
radius_x_recall_mean_opt       0.2020433619
radius_x_recall_median_opt     0.1192560496


Run YQL query (crypta/graph/metrics/stats_base/yql/entropy/entropy.sql)
                                           0
version                                   v1
ts                                1535198400
entropy_x_mobile_total_count        52977495
entropy_x_matched_mobile_count      12201901
entropy_x_coverage              0.2303223473
entropy_x_entropy                2.118892033
entropy_x_entropy_metric        0.1086994258


Run YQL query (crypta/graph/metrics/stats_base/yql/ads/experiment.sql)
                             0
version                     v1
ts                  1535198400
ads_x_rsya_cost_d  7.712996006
```

Можно запускать через санбокс задачу (пример https://sandbox.yandex-team.ru/task/291880585/view)
Результаты смотреть в логах [crypta_task.out.log](https://proxy.sandbox.yandex-team.ru/656722927/crypta_task.out.log)


### Добавление новой метрики

1. Добавить YQL скрипт для подсчета метрик. (Можно расположить например [тут](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/stats_base/lib/yql))
2. Указать скрипт как ресурс в `ya.make` ([тут](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/stats_base/lib/ya.make?rev=3918282#L31-45))
3. Добавить метрику в конфиг `metrics` [`configs/metrics.yaml`](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/stats_base/lib/configs/metrics.yaml)
4. Добавить фикстуры в `ya.make` ([тут](https://a.yandex-team.ru/arc_vcs/crypta/graph/metrics/stats_base/tests/ya.make?rev=r9164121))
5. Смержить и зарелизить ресурс [`CRYPTA_STATS_BASE_METRICS_BUNDLE`](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&forPage=tasks&type=CRYPTA_STATS_BASE_METRICS_BUNDLE)

### Как починить схему, если всё плохо

```bash
export YT_TOKEN=<robot-crypta>

# монтируем таблицу с плохой схемой
yt mount-table //home/crypta/production/graph/stats

# селектим все нужные поля (т.к. там разумное количество строк, можно прямо в локальный текстовый файл)
yt select-rows "ts, version, ads_x_rsya_cost_d, cost_d, ... from [//home/crypta/production/graph/stats]" --format json > out.txt

# создаем новую таблицу с правильной схемой, сразу динамическую
yt create table //home/crypta/production/graph/stats.new --attributes '{"schema" = [{"sort_order"= "ascending"; "required"= false; "type"= "uint64"; "name"= "ts"}; {"sort_order"= "ascending"; "required"= false; "type"= "string"; ...}]; "dynamic" = "true"}'

# монтируем её и вставляем скопированные поля
yt mount-table //home/crypta/production/graph/stats.new
yt insert-rows //home/crypta/production/graph/stats.new --format json < out.txt

# в веб интерфейсе убеждаемся что по строкам вставилось правильно, и заменяем старую таблицу новой
yt remove //home/crypta/production/graph/stats
yt unmount-table //home/crypta/production/graph/stats.new
yt move //home/crypta/production/graph/stats.new //home/crypta/production/graph/stats
```
