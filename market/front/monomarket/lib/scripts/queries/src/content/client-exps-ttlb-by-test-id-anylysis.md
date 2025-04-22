# Расчет TTLB клиентских экспериментов по testid-ам

Анализ клиентского эксперимента. Анализируется TTLB. Данные группируются по сплитам (test-id) и страницам.

Теги: `клиентские эксперименты`, `test id`, `ttlb`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YLT4ehJKfYEUqJnx-fxiAt_3lZozrTJAuohMoOYdIGk=

```sql
use marketclickhouse;

select 
    a.split as split,
    page_id,

    quantileTiming(0.95)(resptime_ms) as TTLB,
    
    uniq(a.req_id) as hits

from (
    select
        host, 
        req_id, 
        resptime_ms,
        page_id,
        arrayJoin([353706, 353709, 353713]) as split
    from market.nginx2
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
        and vhost = 'market.yandex.ru'
        and has(`test_id`, split)
        and page_id in(
            'market:index',
            'market:product', 
            'market:list', 
            'market:search',
            'market:catalog'
        )
) as a

group by a.split, page_id
order by page_id, a.split;
```
