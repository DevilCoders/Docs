# Расчет клиентских экспериментов

Сравнение клиентских метрик по сплита эксперимента на выбранных страницах.

Теги: `клиентские эксперименты`, `ttr`, `tti`, `dcl`, `loaded`.

Ссылка: https://yql.yandex-team.ru/Operations/XwLdz5dg8mTi5L8ExiA50ycSSO0eqVTPKdMim12ugTw=

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
        and host = 'beru.ru'
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
        arrayJoin(['off','lazy']) as split
        
    from market.market_client_timers 
    
    where 
        date between toDate(now() - interval '2' DAY) and toDate(now())
    
        and platform = 'web'
        and vhost = 'beru.ru'
        and name = 'page'
        and page_id in(
            'blue-market:index',
            'blue-market:product', 
            'blue-market:list', 
            'blue-market:cart', 
            'blue-market:search',
            'blue-market:catalog'
        )
        and portion in('firstScreen', 'domContentLoaded', 'loaded')
        and position(info_values[indexOf(info_keys, 'expFlags')], concat('all_speed_lazy-loaded-pics', '=', split)) != 0
) as a

on b.x_market_req_id = a.request_id

group by a.split, page_id
order by page_id;
```
