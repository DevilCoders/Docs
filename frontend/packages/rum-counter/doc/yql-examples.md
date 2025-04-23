## Найти страницы сервиса
```sql
$LOGS = (
    SELECT
        rum_id
    FROM hahn.[home/velocity/rum/1d/2018-03-10]
);

SELECT
    COUNT(*) AS hits,
    rum_id
FROM $LOGS
WHERE rum_id LIKE '%news%'
GROUP BY rum_id
ORDER BY hits DESC;
```
## Найти timeMarks сервиса
```sql
$script = @@
function match(json, str) {
    return JSON.stringify(json).indexOf(str) > -1
}
@@;

$match = Javascript::match("(Yson?, Utf8)->Bool", $script);

SELECT
    time_marks,
    Yson::SerializeText(Yson::YPath(time_marks, "/suggest_js_start")) as suggest_js_start
FROM
    hahn.[home/velocity/rum/1d/2018-07-29]
WHERE
    service == 'portal' AND
    rum_id == 'ru.morda.geotouch' AND
    $match(time_marks, 'suggest')
LIMIT 100
```
## Посчитать процентили по кастомной метрике из timeMarks
```sql
$script = @@
function getTMValue(timeMarks, name) {
    return timeMarks[name];
}
@@;

$getTMValue = Javascript::getTMValue("(Yson?, Utf8)->Int64?", $script);

$LOGS = (SELECT
    $getTMValue(time_marks, 'search_click') as searchClick
FROM
    hahn.[home/velocity/rum/1d/2018-02-02]
WHERE
    service == 'portal' AND
    rum_id == 'ru.morda.geotouch'
);

SELECT
    'searchClick' AS metric,
    CAST(PERCENTILE(searchClick, 0.25) AS INT32) AS p25,
    CAST(PERCENTILE(searchClick, 0.5) AS INT32) AS p50,
    CAST(PERCENTILE(searchClick, 0.75) AS INT32) AS p75,
    CAST(PERCENTILE(searchClick, 0.95) AS INT32) AS p95
FROM $LOGS;
```
## Посчитать гистограммы и процентили по кастомной метрике
```sql
$script = @@
function getMetricValue(obj, name) {
    return obj ? obj[name] : undefined;
}

function getMetricDiff(obj, name1, name2) {
    if (obj) {
        let value1 = obj[name1],
            value2 = obj[name2];

        if (typeof value1 != 'undefined' && typeof value2 != 'undefined') {
            return value1 - value2;
        }
    }
}
@@;

$metricName = 'main_js_duration';
$binSize = 50; -- ширина столбца гистограммы (в мс)
$max = 3000; -- максимальное значение метрики

$getMetricValue = Javascript::getMetricValue("(Yson?, Utf8)->Int64?", $script);
$getMetricDiff = Javascript::getMetricDiff("(Yson?, Utf8, Utf8)->Int64?", $script);

$LOGS = (
    SELECT
        $metricName AS metric_name,
        $getMetricDiff(time_marks, UTF8('main_js_end'), UTF8('main_js_start')) AS metric_value
    FROM
        hahn.[home/velocity/rum/1d/2018-02-03]
    WHERE
        service == 'portal' AND
        rum_id == 'ru.morda.plain'
);

$DATA = (SELECT
    bin AS Position,
    COUNT(*) AS Frequency
FROM $LOGS
WHERE
    metric_value >= 0 AND
    metric_value <= $max
GROUP BY (metric_value / $binSize) AS bin);

$STRUCTS = (
    SELECT
        (
            CAST(Position * $binSize AS Double) ?? 0.0 AS Position,
            CAST(Frequency AS Double) ?? 0.0 AS Frequency
        ) AS Bins,
        Frequency AS hits,
        -1 AS exp
    FROM $DATA);

$script = @@
class Bin(object):
    Frequency = None
    Position = None

def normalize(bins):
    new_bins = []
    summ_frequency = 0
    for bin in bins:
        summ_frequency = summ_frequency + bin.Frequency

    for bin in bins:
        new_bin = Bin()
        new_bin.Frequency = 100.0 * bin.Frequency / summ_frequency
        new_bin.Position = bin.Position
        new_bins.append(new_bin)

    return new_bins
@@;

$normalize = Python::normalize(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>
@@, $script);

$count = Python::count(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
Double
@@,
@@
def count(bins):
    summ = 0;

    for bin in bins:
        summ = summ + bin.Frequency

    return summ
@@);

$BINS = (
    SELECT
        $normalize(LIST(Bins)) AS Bins,
        $count(LIST(Bins)) as hits
    FROM
        $STRUCTS
    GROUP BY exp
);

$HIST = (
    SELECT
        (ListMin(ListExtract(Bins, "Position")) ?? 0.0 AS Min,
        ListMax(ListExtract(Bins, "Position")) ?? 0.0 AS Max,
        ListSum(ListExtract(Bins, "Frequency")) ?? 0.0 AS WeightsSum,
        Bins AS Bins) AS Histogram,
        hits
    FROM $BINS);

SELECT
    Histogram as hist,
    CAST(hits as int32) as hits
FROM $HIST;

SELECT
    $metricName AS metric_name,
    CAST(PERCENTILE(metric_value, 0.25) AS INT32) AS p25,
    CAST(PERCENTILE(metric_value, 0.5) AS INT32) AS p50,
    CAST(PERCENTILE(metric_value, 0.75) AS INT32) AS p75,
    CAST(PERCENTILE(metric_value, 0.95) AS INT32) AS p95,
    COUNT(*) AS hits
FROM
    $LOGS;
```
## Гистограммы и процентили в разбивке по экспериментам
```sql
$script = @@
function getMetricValue(obj, name) {
    return obj ? obj[name] : undefined;
}

function getMetricDiff(obj, name1, name2) {
    if (obj) {
        let value1 = obj[name1],
            value2 = obj[name2];

        if (typeof value1 != 'undefined' && typeof value2 != 'undefined') {
            return value1 - value2;
        }
    }
}
@@;

$metricName = 'ttfb';
$binSize = 50; -- ширина столбца гистограммы (в мс)
$max = 2000; -- максимальное значение метрики

-- формат test_ids - '12345,34567,11111'
$matchExp = Pcre::Grep("21983"); -- id эксперимента
$matchEtalon = Pcre::Grep("21982"); -- id эталона

$getMetricValue = Javascript::getMetricValue("(Yson?, Utf8)->Int64?", $script);
$getMetricDiff = Javascript::getMetricDiff("(Yson?, Utf8, Utf8)->Int64?", $script);

-- выбираем логи своего серивиса из всех логов в самом начале,
-- чтобы потом было меньше вычислений
$LOGS = (
    SELECT
        $metricName AS metric_name,
        $getMetricValue(timing_full, UTF8($metricName)) AS metric_value,
        test_ids
    FROM
        hahn.[home/velocity/rum/1d/2018-02-03]
    WHERE
        service == 'portal' AND
        rum_id == 'ru.morda.geotouch'
);

$MATCHED_LOGS = (
    SELECT
        metric_name,
        metric_value,
        IF($matchExp(test_ids), 1, IF($matchEtalon(test_ids), 0, -1) ) AS exp
    FROM
        $LOGS
);

$DATA = (SELECT
    bin AS Position,
    COUNT(*) AS Frequency,
    exp
FROM $MATCHED_LOGS
WHERE
    exp >= 0 AND
    metric_value >= 0 AND
    metric_value <= $max
GROUP BY exp, (metric_value / $binSize) AS bin);

$STRUCTS = (
    SELECT
        (
            CAST(Position * $binSize AS Double) ?? 0.0 AS Position,
            CAST(Frequency AS Double) ?? 0.0 AS Frequency
        ) AS Bins,
        Frequency as hits,
        exp
    FROM $DATA);

$script = @@
class Bin(object):
    Frequency = None
    Position = None

def normalize(bins):
    new_bins = []
    summ_frequency = 0
    for bin in bins:
        summ_frequency = summ_frequency + bin.Frequency

    for bin in bins:
        new_bin = Bin()
        new_bin.Frequency = 100.0 * bin.Frequency / summ_frequency
        new_bin.Position = bin.Position
        new_bins.append(new_bin)

    return new_bins
@@;

$normalize = Python::normalize(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>
@@, $script);

$count = Python::count(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
Double
@@,
@@
def count(bins):
    summ = 0;

    for bin in bins:
        summ = summ + bin.Frequency

    return summ
@@);

$BINS = (
    SELECT
        $normalize(LIST(Bins)) AS Bins,
        exp,
        $count(LIST(Bins)) as hits
    FROM
        $STRUCTS
    GROUP BY exp);

$HIST = (
    SELECT
        (ListMin(ListExtract(Bins, "Position")) ?? 0.0 AS Min,
        ListMax(ListExtract(Bins, "Position")) ?? 0.0 AS Max,
        ListSum(ListExtract(Bins, "Frequency")) ?? 0.0 AS WeightsSum,
        Bins AS Bins) AS Histogram,
        exp,
        hits
    FROM $BINS);

SELECT
    Histogram as hist,
    exp,
    CAST(hits as int32) as hits
FROM $HIST;

SELECT
    $metricName AS metric_name,
    exp,
    CAST(PERCENTILE(metric_value, 0.25) AS INT32) AS p25,
    CAST(PERCENTILE(metric_value, 0.5) AS INT32) AS p50,
    CAST(PERCENTILE(metric_value, 0.75) AS INT32) AS p75,
    CAST(PERCENTILE(metric_value, 0.95) AS INT32) AS p95,
    COUNT(*) AS hits
FROM
    $MATCHED_LOGS
WHERE
    exp >= 0 AND
    metric_value <= $max
GROUP BY exp
ORDER BY exp DESC;
```

## Метрики по subpages
```sql
use hahn;

$script = @@
function getMetricSubpageTimeMark(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["time_marks"] && obj[page][index]["time_marks"] ? obj[page][index]["time_marks"][name] : undefined;
}

function getMetricSubpageTimeDelta(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["time_deltas"] && obj[page][index]["time_deltas"] ? obj[page][index]["time_deltas"][name] : undefined;
}

function getMetricSubpageLongTaskSum(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["long_task_sum"] ? obj[page][index]["long_task_sum"] : undefined;
}
@@;

$metricName = 'first_paint';
$binSize = 100; -- ширина столбца гистограммы (в мс)
$max = 20000; -- максимальное значение метрики

$getMetricSubpageTimeMark = Javascript::getMetricSubpageTimeMark("(Yson?, Utf8, Int32, Utf8)->Int64?", $script);

$SERVICE_LOGS = (
    SELECT
        *
    FROM
        [//home/velocity/rum/1d/2018-05-30]
    WHERE
        service == 'portal' and
        rum_id == 'ru.morda.plain'
);

$LOGS = (
    SELECT
        $metricName AS metric_name,
        $getMetricSubpageTimeMark(subpages, 'ru.morda.player.tv', 0, UTF8($metricName)) AS metric_value
    FROM
        $SERVICE_LOGS
);

SELECT
    $metricName AS metric_name,
    CAST(PERCENTILE(metric_value, 0.25) AS INT32) AS p25,
    CAST(PERCENTILE(metric_value, 0.5) AS INT32) AS p50,
    CAST(PERCENTILE(metric_value, 0.75) AS INT32) AS p75,
    CAST(PERCENTILE(metric_value, 0.95) AS INT32) AS p95,
    LinearHistogram(metric_value) as hist,
    COUNT(*) AS hits
FROM
    $LOGS
WHERE
    metric_value <= $max and
    metric_value >= 0
```
## Гистограммы и процентили для метрик subpage в разбивке по экспериментам
```sql
use hahn;

$script = @@
function getMetricSubpageTimeMark(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["time_marks"] && obj[page][index]["time_marks"] ? obj[page][index]["time_marks"][name] : undefined;
}

function getMetricSubpageTimeDelta(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["time_deltas"] && obj[page][index]["time_deltas"] ? obj[page][index]["time_deltas"][name] : undefined;
}

function getMetricSubpageLongTaskSum(obj, page, index, name) {
    return obj && obj[page] && obj[page][index]["long_task_sum"] ? obj[page][index]["long_task_sum"] : undefined;
}
@@;

$metricName = 'player_init';
$binSize = 100; -- ширина столбца гистограммы (в мс)
$max = 20000; -- максимальное значение метрики

$matchExp = Pcre::Grep("117786"); -- id эксперимента
$matchEtalon = Pcre::Grep("117781"); -- id эталона

$getMetricSubpageTimeMark = Javascript::getMetricSubpageTimeMark("(Yson?, Utf8, Int32, Utf8)->Int64?", $script);

$SERVICE_LOGS = (
    SELECT
        *
    FROM
        [//home/velocity/rum/1d/2019-02-08]
    WHERE
        service == 'portal' and
        rum_id == 'ru.morda.plain'
);

$MATCHED_LOGS = (
    SELECT
        $metricName AS metric_name,
        $getMetricSubpageTimeMark(subpages, 'stream', 0, UTF8($metricName)) AS metric_value,
        IF($matchExp(test_ids), 1, IF($matchEtalon(test_ids), 0, -1) ) AS exp
    FROM
        $SERVICE_LOGS
);

$DATA = (SELECT
    bin AS Position,
    COUNT(*) AS Frequency,
    exp
FROM $MATCHED_LOGS
WHERE
    exp >= 0 AND
    metric_value >= 0 AND
    metric_value <= $max
GROUP BY exp, (metric_value / $binSize) AS bin);

$STRUCTS = (
    SELECT
        (
            CAST(Position * $binSize AS Double) ?? 0.0 AS Position,
            CAST(Frequency AS Double) ?? 0.0 AS Frequency
        ) AS Bins,
        Frequency as hits,
        exp
    FROM $DATA);

$script = @@
class Bin(object):
    Frequency = None
    Position = None

def normalize(bins):
    new_bins = []
    summ_frequency = 0
    for bin in bins:
        summ_frequency = summ_frequency + bin.Frequency

    for bin in bins:
        new_bin = Bin()
        new_bin.Frequency = 100.0 * bin.Frequency / summ_frequency
        new_bin.Position = bin.Position
        new_bins.append(new_bin)

    return new_bins
@@;

$normalize = Python::normalize(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>
@@, $script);

$count = Python::count(@@
(List<
    Struct<
        Frequency:Double,
        Position:Double
    >
>) ->
Double
@@,
@@
def count(bins):
    summ = 0;

    for bin in bins:
        summ = summ + bin.Frequency

    return summ
@@);

$BINS = (
    SELECT
        $normalize(LIST(Bins)) AS Bins,
        exp,
        $count(LIST(Bins)) as hits
    FROM
        $STRUCTS
    GROUP BY exp);

$HIST = (
    SELECT
        (ListMin(ListExtract(Bins, "Position")) ?? 0.0 AS Min,
        ListMax(ListExtract(Bins, "Position")) ?? 0.0 AS Max,
        ListSum(ListExtract(Bins, "Frequency")) ?? 0.0 AS WeightsSum,
        Bins AS Bins) AS Histogram,
        exp,
        hits
    FROM $BINS);

SELECT
    Histogram as hist,
    exp,
    CAST(hits as int32) as hits
FROM $HIST;

SELECT
    $metricName AS metric_name,
    exp,
    CAST(PERCENTILE(metric_value, 0.25) AS INT32) AS p25,
    CAST(PERCENTILE(metric_value, 0.5) AS INT32) AS p50,
    CAST(PERCENTILE(metric_value, 0.75) AS INT32) AS p75,
    CAST(PERCENTILE(metric_value, 0.95) AS INT32) AS p95,
    COUNT(*) AS hits
FROM
    $MATCHED_LOGS
WHERE
    exp >= 0 AND
    metric_value <= $max
GROUP BY exp
ORDER BY exp DESC;
```
