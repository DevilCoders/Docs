# Статистика сброса statusBsSynced по бинлогам

Для проверки гипотез о повышенной или необычной нагрузке на транспорт в БК
можно посмотреть статистику из бинлогов по количеству изменений поля `statusBsSynced` на значение `No` разными трейс-методами.

## YQL запрос
{% cut "Текст YQL запроса" %}

```yql
USE hahn;


$date_from = '2020-07-06';
$date_to = '2020-07-18';
$rest_share = 0.03; -- доля, ниже которой запросы засчитываются в общий rest
$step = Interval('PT3H'); -- интервал группировки по времени
$format = DateTime::Format("%Y-%m-%d %H:%M:%S");

$parse = ($yson) -> {
    $filter_status_bs_synced = ($el) -> {
        RETURN Yson::LookupString($el, 'name') == 'statusBsSynced';
    };
    $extract_status_bs_synced = ($el) -> {
        $raw = Yson::YPath($el, '/value/string');
        $str = Yson::ConvertToString($raw);
        RETURN Unwrap($str);
    };
    $parse_el = ($el) -> {
        $id = Yson::ConvertToInt64(Yson::YPath($el, '/primary_key/0/value/integer'));
        $after = Yson::ConvertToList(Yson::YPath($el, '/after'));
        $filtered = ListFilter($after, $filter_status_bs_synced);
        $statuses = ListMap($filtered, $extract_status_bs_synced);
        RETURN AsStruct($id AS id, ListHead($statuses) AS statusBsSynced);
    };
    $elements = Yson::ConvertToList($yson);
    RETURN ListMap($elements, $parse_el);
};

$schema = Struct<`timestamp`:Int64
    , `table`:String
    , operation:String?
    , trance_info_method:String?
    , rows:Yson
    , resharding:Bool?
>;

$logs = SELECT *
FROM RANGE(`//home/logfeller/logs/direct-ppcdata-binlog-log/1d`, $date_from, $date_to)
WITH SCHEMA $schema
UNION ALL
SELECT *
FROM RANGE(`//home/logfeller/logs/direct-ppcdata-binlog-log/30min`, $date_from, $date_to)
WITH SCHEMA $schema
;

$data = SELECT t
    , method
    , type
    , COUNT(*) AS cnt
FROM (
    SELECT row.id AS id
        , row.statusBsSynced AS statusBsSynced
        , method
        , type
        , DateTime::FromSeconds(Cast(t AS Uint32) + 3600u * 3u) AS time
    FROM (
        SELECT `timestamp` AS t
            , operation
            , `table` AS type
            , trance_info_method AS method
            , $parse(`rows`) AS rows
        FROM $logs
        WHERE `table` IN ('campaigns', 'phrases', 'banners', 'bids')
            AND (operation IS NULL OR operation = 'UPDATE')
            AND (resharding IS NULL OR NOT resharding)
        -- LIMIT 150000
    )
    FLATTEN LIST BY rows AS row
    WHERE row.statusBsSynced = 'No'
)
GROUP BY $format(DateTime::StartOf(time, $step)) AS t, method, type
;

$totals = SELECT t
    , type
    , SUM(cnt) AS total
FROM $data
GROUP BY t, type
;

$times = SELECT DISTINCT t
FROM $totals
;

$top_methods = SELECT type, method
FROM (
    SELECT IF(CAST(d.cnt AS Double) / t.total > $rest_share, d.method, 'rest') AS method
        , d.type AS type
    FROM $data AS d
    JOIN $totals AS t ON t.t = d.t AND t.type = d.type
)
GROUP BY method, type
;

$top_data = SELECT t
    , type
    , method
    , SUM(cnt) AS cnt
FROM (
    SELECT d.t AS t
        , d.type AS type
        , IF(tm.method IS NOT NULL, d.method, 'rest') AS method
        , d.cnt AS cnt
    FROM $data AS d
    LEFT JOIN $top_methods AS tm ON tm.method = d.method AND tm.type = d.type
)
GROUP BY t, type, method
;

$result = SELECT t.t AS t
    , tm.type AS type
    , tm.method AS method
    , NVL(td.cnt, 0) AS cnt
FROM $times AS t
CROSS JOIN $top_methods AS tm
LEFT JOIN $top_data AS td ON td.t = t.t AND td.method = tm.method AND td.type = tm.type
;

DEFINE ACTION $stat($table) AS
    SELECT t, method, cnt
    FROM $result
    WHERE type = $table
    ORDER BY t, method;
END DEFINE;

/* у YQL есть ограничение на отдачу данных для графиков: около 2 тысяч точек
поэтому если у вас много данных — выбирать лучше по одному
если мало (например всего пара дней) — можно все сразу */

DO $stat('campaigns');
-- DO $stat('phrases');
DO $stat('banner');
-- DO $stat('bids');
```

{% endcut %}

В запросе нужно поменять:
- `$date_from` — с какой даты строить график
- `$date_to` — по какую дату строить график
- `$rest_share` — доля запросов (за окно времени) конкретного trace—метода от всех, ниже которой они засчитывается как метод "rest"
- `$step` — окно времени для группировки

Подробнее про `$rest_share`:
- если у trace-метод в любом окне времени доля запросов выше порога — он всегда будет показан на графике
- если во всех окнах — ниже, то запросы этого метода попадут в общий "rest"


{% note info "Особенности выполнения запроса" %}

Для статистики за три дня — запрос работает около получаса, за 11 дней — 45 минут.  
Пересчет при смене `$rest_share` или таблицы выполняется за 5—10 минут.  
Смена окна времени — приводит к полному пересчёту.

{% endnote %}

## Графики
Для построения графика по результату YQL запроса, нужно:
1. Перейти на таб **Chart** (с нужным номером, если их несколько)
1. Выбрать **Chart type:** `Pivot`
1. **Categories:** `t`
1. **Series:** `method`
1. **Values:** `cnt`
1. Поставить галочку **Interpret X axis as timeline**
1. Выбрать **Series type:** `area` или `areaspline`
1. Выбрать **Stacking:** `normal`
Готово!

## Примеры
Запрос за 6 — 18 июля, таблицы [phrases и bids](https://yql.yandex-team.ru/Operations/X7-jsGim9VhRBFo11-BPX0S8VQx5vf9JyUMvnBYMqOI=),
[campaigns и banners](https://yql.yandex-team.ru/Operations/X7-vqJ3udghi-B5IcatmxCzIfE_UCYfCEislG0lSZ9c=).
Из них получаются вот такие графики:
<iframe markdown="1" frameborder="0" width="100%" height="400px" src="https://charts.yandex-team.ru/preview/editor/pet3ekhclo8wk?_embedded=1"></iframe>
<iframe markdown="1" frameborder="0" width="100%" height="400px" src="https://charts.yandex-team.ru/preview/editor/1q57ngvoxcwww?_embedded=1"></iframe>
<iframe markdown="1" frameborder="0" width="100%" height="400px" src="https://charts.yandex-team.ru/preview/editor/pet5mc03b32sk?_embedded=1"></iframe>
<iframe markdown="1" frameborder="0" width="100%" height="400px" src="https://charts.yandex-team.ru/preview/editor/5u9kd2e7y5a80?_embedded=1"></iframe>

_(на части графиков правая часть обрезана — влезло только 1000 точек)_

## Отладка запроса
Запрос легко адаптировть и для других полей/таблиц, для может потребоваться поменять тип значения колонки (путь в бинлоге `/value/string` и YSON-тип).

Чтобы отладка не была мучительно долгой, советую:
1. Ограничить входные данные одной таблицей, например задав `$date_from` и `$date_to` равными дате за позавчера
1. Добавить лимит в несколько сотен тысяч строк в подзапрос данных (в примере он есть, но закомментирован)
1. Включить другой движок выполнения запроса, указав в начале
    ```yql
    PRAGMA DqEngine = 'force';
    ```
1. Если будет падать с ошибкой
    ```text
    yql/providers/dq/provider/yql_dq_exectransformer.cpp:778  HandlePull(): requirement tasks.size() <= State->Settings->MaxTasksPerOperation.Get().GetOrElse(70) failed
    ```
    то можно подкрутить настройки, добавив прагму:
    ```yql
    PRAGMA dq.MaxTasksPerOperation='200';
    ```

{% endnote %}
