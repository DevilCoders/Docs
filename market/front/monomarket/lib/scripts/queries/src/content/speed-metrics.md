# Метрики скорости

Серверные и клиентские метрики скорости сервиса.

Теги: `метрики скорости`, `ttlb`, `ttr`, `tti`, `dcl`, `loaded`.

Ссылка: https://yql.yandex-team.ru/Operations/YVap5tK3DHqKY_UyNPWVr3bLB48HRGPevXhn7YuedXE=

```sql
use marketclickhouse;

select
    quantileTimingIf(0.95)(resptime_ms, portion = 'firstScreen') as TTLB,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded

from (
    select
        timestamp,
        timestamp_ms,
        start_time_ms,
        duration_ms,
        portion,
        request_id
    from market.market_client_timers
    where date = today()
        and vhost = 'market.yandex.ru'
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())     
) as timers

left join (
    select
        host, req_id, resptime_ms
    from market.nginx2
    where date = today()
        and vhost = 'market.yandex.ru'
        aand timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
) as nginx
    on timers.request_id = nginx.req_id
```
