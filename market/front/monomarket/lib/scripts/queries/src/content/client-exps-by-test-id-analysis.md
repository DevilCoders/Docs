# Расчет клиентских метрик клиентских экспериментов по testid-ам

Анализ клиентского эксперимента. Анализируются клиентские метрики. Данные группируются по сплитам (test-id) и страницам. 

Теги: `клиентские эксперименты`, `test id`, `ttr`, `tti`, `dcl`, `loaded`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YLTvpfMBw877XKd6Dg3XHcU1cj2HDKj3TPG-z8LUDjk=

```sql
use marketclickhouse;

select 
    a.split as split,
    page_id,
    
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded,
    
    uniq(a.request_id) as hits

from (
    select 
        x_market_req_id
    from market.slb_balancer
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
        and host = 'market.yandex.ru'
        and method = 'GET'
        and is_robot = 'false'
) as b

inner join (
    select 
        request_id,
        page_id, 
        portion, 
        timestamp_ms, 
        start_time_ms, 
        duration_ms,
        arrayJoin(['353706','353709', '353713']) as split
        
    from market.market_client_timers 
    
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
    
        and platform = 'web'
        and vhost = 'market.yandex.ru'
        and name = 'page'
        and page_id in(
            'market:index',
            'market:product', 
            'market:list', 
            'market:search',
            'market:catalog'
        )
        and portion in('firstScreen', 'domContentLoaded', 'loaded')
        and position(info_values[indexOf(info_keys, 'testIds')], split) != 0
) as a

on b.x_market_req_id = a.request_id

group by a.split, page_id
order by page_id, a.split
```
