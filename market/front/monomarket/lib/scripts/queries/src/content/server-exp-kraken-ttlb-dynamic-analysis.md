# Анализ динамики TTLB в ходе серверннго эксперимента на Кракене

Позволяет оценить влияние включения/отключения серверного эксперимента на Кракене. По таблице можно построить удобный график.

Теги: `ttlb`, `серверные эксперименты`, `метрики скорости`, `кракен`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbaPhJKfZcFg_z5HBfuGllS_GvuAEMU92EKdK-0Lsk=

```sql
use marketclickhouse;

select
    x,
    round(quantile(0.99)(resptime_ms)) as ttlb99
from (
    select
        *,
        toStartOfFiveMinute(toDateTime(timestamp)) as x
    from market.nginx2
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and host in (
            'vla3-1713-ab3-vla-market-prod-f-e0b-8041.gencfg-c.yandex.net'
        )
        and service = 'desktop'
        and page_id = 'market:search'
)
group by x
order by x;
```
