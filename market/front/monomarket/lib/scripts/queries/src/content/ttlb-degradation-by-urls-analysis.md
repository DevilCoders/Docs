# Анализ деградации TTLB на урлах

Запрос позволяет увидеть, на каких урлах случилась деградация TTLB.

Теги: `анализ деградации`, `ttlb`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbTXAVK8P1EbnkK-QfRqyVH2e8wE_sAWA82vQraDu8=

```sql
use marketclickhouse;

select 
    url,

    current_p99,
    prev_p99,
    current_p99 - prev_p99 as delta_p99,

    current_hits,
    prev_hits,
    current_hits - prev_hits as delta_hits
  from (
    select
        count() as current_hits,
        quantileTiming(0.99)(resptime_ms) as current_p99,
        url
      from market.nginx2
     where (
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and page_id = 'market:list'
    )
     group by url
    having current_hits > 100
     order by current_p99 desc
) as current left join (
    select
        count() as prev_hits,
        quantileTiming(0.99)(resptime_ms) as prev_p99,
        url
      from market.nginx2
     where (
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and page_id = 'market:list'
    )
     group by url
    having prev_hits > 100
     order by prev_p99 desc
) as previous
    on current.url = previous.url
 where prev_hits != 0
   and current_hits != 0
 order by delta_p99 desc, delta_hits desc;
```
