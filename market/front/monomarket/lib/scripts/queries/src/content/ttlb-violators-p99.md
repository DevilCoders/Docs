# Главные превышатели 99 перцентиля TTLB

Собирает страничные данные по TTLB, грамотно собирает данные о вызове ремоут-резолверов.

Теги: `ttlb`, `resolver`, `резолвер`.

Ссылка: https://yql.yandex-team.ru/Operations/YVamJK5ODy4UJXj-9jpxfp76Yve759EaYxN7CzlzmwY=

```sql
use marketclickhouse;

select
    arrayJoin(resource) as res,
    count() as cnt
from (
    with (
        select
            count()
        from market.nginx2
        where date = today()
            and vhost = 'market.yandex.ru'
            and timestamp > now() - 3600
            and http_code = 200
            and suspiciousness = ''
            and page_id != ''
    ) as TOTAL

    select if(
        page_id = 'api:resolve', 
        arrayMap(x -> concat('resolve:', splitByChar('=', x)[2]), extractURLParameters(url)), 
        [page_id]
    ) as resource
        
    from market.nginx2
    where date = today()
        and vhost = 'market.yandex.ru'
        and timestamp > now() - 3600
        and http_code = 200
        and suspiciousness = ''
        and page_id != ''
    
    order by resptime_ms desc
    
    limit toUInt64(ceil(TOTAL * (1 - 0.99)))
)
group by res
order by cnt desc;
```
