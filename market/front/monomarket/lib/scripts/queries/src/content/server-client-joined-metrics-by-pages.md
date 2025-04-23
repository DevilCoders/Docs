# TTLB, TTR и TTI по сервисам и страницам

Большая таблица с аггрегацией всех основных метрик по сервисам и страницам.
Позволяет удобно взглянуть на клиентские метрики страницы по хостам.

Теги: `агрегированная метрика`, `ttr`, `tti`, `ttlb`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbb45fFtzcrh8hpyGOZKKw-e8UXJGqzl8wX_tIP_pI=

```sql
use marketclickhouse;

select
    request_id,
    timestamp,
    host,
    service,
    page_id,
    request_TTLB,
    request_TTR,
    request_TTI
from (
    select
        timestamp,
        page_id,
        service,
        timestamp_ms - start_time_ms as request_TTR,
        timestamp_ms - start_time_ms + duration_ms as request_TTI,
        request_id
    from `market`.`market_client_timers`
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and service in ('market_front_desktop', 'market_front_touch')
        and name = 'page'
        and portion = 'firstScreen'
        and request_id != ''
) as client_timers inner join (
    select
        host,
        req_id as request_id,
        resptime_ms as request_TTLB
    from market.nginx2
    where 
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and service in ('desktop', 'touch')
        and req_id != ''
        and resptime_ms != 0
) as server_timers
on client_timers.request_id = server_timers.request_id;
```
