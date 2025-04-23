# Метрика с разбивкой на бакеты

Строит последовательность метрики TTI с интервалом в 10 минут, разбитую на бакеты.

Квантили не всегда удобны для анализа, особенно когда изменяется rps. Если требуется исследовать ухудшились/улучшились временные метрики или добавилось/убавилось быстрых/медленных запросов стоит проверить графики с разбивкой по бакетам - подсчёт количества запросов для которых метрика укладывается в некий интервал. Бакеты можно выбирать произвольные, но обычно удобнее всего использовать логарифмическую шкалу.

Теги: `бакеты`, `сплиттинг`, `tti`.

Ссылка: https://yql.yandex-team.ru/Operations/YVarg5fFtzcrh6axcG4GLmoiBIfiNkMG0JAbLsn2fKg=

```sql
use marketclickhouse;

select 
    toStartOfTenMinutes(toDateTime(timestamp)) as time, 
    pow(2, ceil(log2(timestamp_ms - start_time_ms + duration_ms))) as bucket, 
    count() as cnt
from market.market_client_timers
where date = today()
    and vhost = 'market.yandex.ru'
    and portion = 'firstScreen'
    and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
    
group by time, bucket
order by bucket desc, time asc;
```
