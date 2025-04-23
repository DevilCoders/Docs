# Метрика TTR с динамикой по времени

Строит список ВРЕМЯ - TTR с интервалом в пять минут.

Теги: `метрики скорости`, `ttr`.

Ссылка: https://yql.yandex-team.ru/Operations/YVaq8ZfFtzcrh6ZF76uSi9nAyeZZDNFEAr5XgBSUL7k=

```sql
use marketclickhouse;

select
    toStartOfFiveMinute(toDateTime(timestamp)) as time,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR

from market.market_client_timers
where date = today()
    and vhost = 'market.yandex.ru'
    and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())

group by time
order by time asc;
```
