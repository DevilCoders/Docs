# Ошибки подключения к базе данных
Запросы, с помощью которых можно определить период недоступности БД по ошибкам подключения к ней из messages—лога.

## ppc
Выбирает ошибки подключения к любому шарду ppc из perl и недоступность соединения в connection pool для java.
Удобно группирует число ошибок по шардам и минутам.
Для каждого шарда указано число ошибок в нём, первая и последняя секунды с ошибкой.

Готовый [YQL—запрос](https://yql.yandex-team.ru/Operations/YCvAx1J2-RfYnIKaldEsCvBrzBEo2F3CNbhiuINpqT0=).  
В запросе стоит поменять дату и время на нужные.

### запрос в clickhouse
```yql
-- поменяйте дату и время ниже
SELECT minute
    , arrayMap(
        (x, y, f, l) -> format('{0}: {1} ({2} — {3})', toString(x), toString(y), f, l)
        , groupArray(shard)
        , groupArray(errors)
        , groupArray(first_sec)
        , groupArray(last_sec)
    ) as stat
    , sum(errors) AS all_errors
FROM (
    SELECT substring(toString(toStartOfMinute(log_time)), 12, 5) AS minute
        , toUInt16OrZero(if(shard_perl = '', shard_java, shard_perl)) AS shard
        , uniqExact(span_id) AS errors
        , substring(toString(min(log_time)), 18, 2) AS first_sec
        , substring(toString(max(log_time)), 18, 2) AS last_sec
    FROM (
        SELECT log_time
            , extract(extract(message, 'ppc_[0-9]+_+[0-9]+ - Connection is not available'), '[0-9]+') as shard_java
            , extract(extract(message, 'ppc:[0-9]+:'), '[0-9]+') AS shard_perl
            , span_id
        FROM messages
        WHERE log_date = '2020-11-09'   -- задайте свою дату и время
        AND log_time BETWEEN '2020-11-09 10:30:00' AND '2020-11-09 14:00:00'
        AND (message LIKE '%Connection is not available%' AND message NOT LIKE '%ppcdict%'
            OR message LIKE 'Can\'t %' AND message LIKE '%ppc:%')
    )
    GROUP BY minute, shard
    HAVING errors > 3
    ORDER BY minute, shard
)
GROUP BY minute
ORDER BY minute
```

### пример результата
minute | stat | all_errors
:--- | :--- | :---
"11:28" | [<br/>"9: 4 (08 — 51)"<br/>] | 4
"11:29" | [<br/>"9: 5 (14 — 47)"<br/>] | 5
"11:30" | [<br/>"8: 9 (11 — 55)",<br/>"9: 77 (04 — 59)"<br/>] | 86
"11:31" | [<br/>"8: 16 (06 — 59)",<br/>"9: 138 (00 — 59)"<br/>] | 154
"11:32" | [<br/>"8: 48 (05 — 59)",<br/>"9: 167 (01 — 59)"<br/>] | 215
"11:33" | [<br/>"1: 127 (27 — 59)",<br/>"8: 117 (00 — 59)",<br/>"9: 313 (00 — 59)"<br/>] | 557


## ppcdict
Выбирает ошибки подключения к ppcdict из perl и недоступность соединения в connection pool для java.

Готовый [YQL](https://yql.yandex-team.ru/Operations/YCp4qfMBw4rPTKWmkI0x38Aue_696LuWq8H37GvSWSs=).  
В запросе можно поменять:
- группировку по времени (в примере — 10 секунд)
- дату и диапазон времени (в примере — с 6:20 до 8:30 6го февраля)
- фильтрацию разовых ошибок (в примере — исключаются интервалы времени всего с одной ошибкой)

### запрос в clickhouse
```yql
SELECT toStartOfInterval(log_time, INTERVAL 10 second) AS t
    , uniqExact(span_id) AS errors
    , min(log_time) AS first
    , max(log_time) AS last
    , arrayStringConcat(arraySort(groupUniqArray(h)), ', ') AS hosts
FROM (
    SELECT log_time
        , span_id
        , if(host LIKE 'direct-java-jobs-%', 'jobs',
            if (host LIKE 'direct-java-intapi-%', 'intapi-java', 
                if (host LIKE 'direct-perl-frontends-%', 'web-perl', 
                    if (host LIKE 'direct-java-api5-%', 'api-java',
                        if(host LIKE 'direct-perl-soap-%', 'api-perl',
                            if (host LIKE 'direct-perl-intapi-%', 'intapi-perl',
                                if (host LIKE 'direct-java-web-%', 'web-java',
                                    'rest'
                                    -- substring(host, 1, 18)
                                )
                            )
                        )
                    )
                )
            )
        ) AS h
    FROM messages
    WHERE log_date = '2021-02-06'
    AND log_time BETWEEN '2021-02-06 06:20:00' AND '2021-02-06 08:30:00'
    AND (message LIKE '%ppcdict% - Connection is not available%'
        OR message LIKE 'Can\'t %' AND message LIKE '%ppcdict%')
)
GROUP BY t
HAVING errors > 1
ORDER BY t
```

### пример результата
t | errors | first | last | hosts
:--- | :---: | :--- | :--- | ---: 
"2021-02-06 07:04:00" | 1222 | "2021-02-06 07:04:00" | "2021-02-06 07:04:09" | "jobs"
"2021-02-06 07:04:10" | 1238 | "2021-02-06 07:04:10" | "2021-02-06 07:04:19" | "jobs"
"2021-02-06 07:04:20" | 1348 | "2021-02-06 07:04:20" | "2021-02-06 07:04:29" | "intapi-java, jobs"
"2021-02-06 07:04:30" | 1272 | "2021-02-06 07:04:30" | "2021-02-06 07:04:39" | "intapi-java, jobs"
"2021-02-06 07:04:40" | 1252 | "2021-02-06 07:04:40" | "2021-02-06 07:04:49" | "intapi-java, jobs"
"2021-02-06 07:04:50" | 1313 | "2021-02-06 07:04:50" | "2021-02-06 07:04:59" | "intapi-java, jobs"
"2021-02-06 07:05:00" | 1286 | "2021-02-06 07:05:00" | "2021-02-06 07:05:09" | "intapi-java, jobs"
"2021-02-06 07:05:10" | 1194 | "2021-02-06 07:05:10" | "2021-02-06 07:05:19" | "intapi-java, jobs"
"2021-02-06 07:05:20" | 1295 | "2021-02-06 07:05:20" | "2021-02-06 07:05:29" | "intapi-java, jobs, web-perl"
_показа только часть вывода_
