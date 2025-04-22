# Метрики скорости в разрезе по test_id

Если нужно найти деградации скорости в экспах.

Теги: `метрики скорости`, `ttr`, `tti`, `ttlb`.

Ссылка: https://yql.yandex-team.ru/Operations/YcruDJfFtwRbFhbVdIM_J6OUwxeN_E1HKXHHIlqK2p0=

```sql
USE marketclickhouse;

SELECT
    quantileTiming(0.95)(timestamp_ms - start_time_ms) as ttr,
    quantileTiming(0.95)(timestamp_ms - start_time_ms + duration_ms) as tti,

    arrayJoin(splitByChar(',', info_values[indexOf(info_keys, 'testIds')])) as "test_id",
    count(*)
FROM market.market_client_timers
WHERE 
    date = '2021-12-28'
    and timestamp >= toUnixTimestamp('2021-12-28 00:00:00')
    and timestamp <= toUnixTimestamp('2021-12-28 00:01:00') 
    AND service = 'market_front_touch'
    and name = 'page'
    and portion = 'firstScreen'
    and page_id = 'touch:index'
group by test_id
```

Более сложный запрос, который позволяет посмотреть и на TTLB.

Ссылка: https://yql.yandex-team.ru/Operations/YUhbwgVK8HLJX9EEr8g77zXzN_agQIYPzfhNW-90HOo=

```sql
use marketclickhouse;

select
    page_id,
    test_id,
    quantileTiming(0.99)(request_TTLB) as TTLB99,
    quantileTiming(0.95)(request_TTR) as TTR95,
    quantileTiming(0.95)(request_TTI) as TTI95,
    count() as cnt
from (
    select
        request_id,
        timestamp,
        host,
        service,
        page_id,
        request_TTLB,
        request_TTR,
        request_TTI,
        test_id
    from (
        select
            timestamp,
            page_id,
            service,
            timestamp_ms - start_time_ms as request_TTR,
            timestamp_ms - start_time_ms + duration_ms as request_TTI,
            request_id
        from `market`.`market_client_timers`
        where date = toDate('2021-09-20')
        and service in ('market_front_desktop', 'market_front_touch')
        and timestamp > toUnixTimestamp('2021-09-20 11:00:00')
        and timestamp < toUnixTimestamp('2021-09-20 12:00:00')
        and name = 'page'
        and portion = 'firstScreen'
        and request_id != ''
        and page_id in ('market:index', 'touch:index')
    ) as client_timers inner join (
        select
            host,
            req_id as request_id,
            resptime_ms as request_TTLB,
            if(empty(test_id), [0], test_id) as test_id
        from market.nginx2
        where date = toDate('2021-09-20')
        and timestamp > toUnixTimestamp('2021-09-20 11:00:00')
        and timestamp < toUnixTimestamp('2021-09-20 12:00:00')
        and environment = 'PRODUCTION'
        and service in ('desktop', 'touch')
        and req_id != ''
        and resptime_ms != 0
    ) as server_timers
    on client_timers.request_id = server_timers.request_id
)
array join test_id
group by page_id, test_id
order by page_id, TTLB99 desc;
```