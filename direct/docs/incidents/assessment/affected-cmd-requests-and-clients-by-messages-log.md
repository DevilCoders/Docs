# Веб-интерфейс: запросы и клиенты по ошибке из messages
Запрос позволяет посчитать (в разбивке по дням + общая статистика за все дни):

{% include [what](_includes/what-affected-by-messages.md)%}

## YQL запрос
[YQL](https://yql.yandex-team.ru/Operations/XyPf8hpqvxyECPi0UA8g27F-hzfmB7RqqfDU5H69FWI=).
В запросе нужно изменить даты и текст ошибки, по которому запросы ищутся в messages-логе.  
Текст нужно вписывать `@@%` вот так `%@@`.
Собачки — границы строки, проценты — для LIKE-поиска.

```yql
USE hahn;
PRAGMA DisableAnsiInForEmptyOrNullableItemsCollections;

-- отредактируйте эту часть
$date_from = '2020-04-16';
$date_to = '2020-04-24';
$message = @@%Cannot return null for non-nullable type: 'String' within parent 'GdClientMetrikaCounter' (/client/metrikaCountersWithAdditionInformation/counters[%]/name%@@;
------

$src = SELECT log_time, trace_id, method
FROM RANGE(`//home/direct/logs/messages_log`, $date_from, $date_to)
WHERE message LIKE $message;

$ids = SELECT DISTINCT trace_id FROM $src;
$methods = SELECT DISTINCT cmd FROM RANGE(`//home/direct/logs/ppclog_cmd`, $date_from, $date_to) WHERE reqid IN $ids;

$data = SELECT log_date
    , with_error
    , clients_count
    , requests_count
    , first
    , last
FROM (
    SELECT log_date
        , with_error
        , COUNT(DISTINCT ClientID) AS clients_count
        , COUNT(*) AS requests_count
        , MIN(log_time) AS first
        , MAX(log_time) AS last
    FROM (
        SELECT log_date
            , log_time
            , ClientID
            , with_error
        FROM (
            SELECT SUBSTRING(log_time, 0, 10) AS log_date
                , log_time
                , ListHead(Yson::ConvertToUint64List(cluid, Yson::Options(true AS AutoConvert))) AS uid
                , reqid IN $ids AS with_error
            FROM RANGE(`//home/direct/logs/ppclog_cmd`, $date_from, $date_to)
            WHERE cmd IN $methods
        ) AS l
        JOIN LIKE(`//home/direct/mysql-sync/current`, `ppc:%`, `straight/users`) AS u ON u.uid = l.uid
    )
    GROUP BY CUBE (log_date, with_error)
)
WHERE with_error IS NULL
    OR with_error = True
;

$prepared = SELECT NVL(log_date, '0000-00-00') AS log_date
    , with_error
    , clients_count
    , requests_count
    , first
    , last
FROM $data;

SELECT a.log_date AS log_date
    , Math::Round(NVL(e.clients_count, 0) * 100.0 / a.clients_count, -2) AS clients_pct
    , NVL(e.clients_count, 0) AS clients_error
    , a.clients_count AS clients_all
    , Math::Round(NVL(e.requests_count, 0) * 100.0 / a.requests_count, -2) AS requests_pct
    , NVL(e.requests_count, 0) AS requests_error
    , a.requests_count AS requests_all
    , e.first AS first_error
    , e.last AS last_error
FROM $prepared AS a
LEFT JOIN $prepared AS e ON e.log_date = a.log_date
WHERE a.with_error IS NULL
    AND e.with_error = True
ORDER BY log_date
```

## пример результата

log_date | clients_pct | clients_error | clients_all | requests_pct | requests_error | requests_all | first_error | last_error
:---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:
0000-00-00 | 0.57 | 486 | 84987 | 0.66 | 3049 | 459533 | 2020-04-16 15:07:07 | 2020-04-23 16:48:49
2020-04-16 | 0.38 | 71 | 18590 | 0.48 | 270 | 56356 | 2020-04-16 15:07:07 | 2020-04-16 23:46:13
2020-04-17 | 0.68 | 120 | 17536 | 0.82 | 466 | 56548 | 2020-04-17 00:02:07 | 2020-04-17 23:54:36
2020-04-18 | 0.68 | 68 | 9967 | 0.73 | 225 | 30936 | 2020-04-18 00:00:30 | 2020-04-18 23:42:19
2020-04-19 | 0.71 | 63 | 8828 | 0.93 | 253 | 27246 | 2020-04-19 00:07:56 | 2020-04-19 23:59:53
2020-04-20 | 0.7 | 138 | 19750 | 0.93 | 546 | 58910 | 2020-04-20 01:11:35 | 2020-04-20 23:57:16
2020-04-21 | 0.86 | 170 | 19767 | 0.73 | 427 | 58102 | 2020-04-21 00:01:43 | 2020-04-21 23:54:41
2020-04-22 | 0.68 | 133 | 19456 | 0.79 | 466 | 58670 | 2020-04-22 00:09:10 | 2020-04-22 23:59:54
2020-04-23 | 0.59 | 112 | 18980 | 0.7 | 396 | 56959 | 2020-04-23 00:01:00 | 2020-04-23 16:48:49
