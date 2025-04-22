# JOIN запросов в nginx и ошибок приложения по requestId

Агрегирует данные из таблицы ошибок с таблицей nginx2.

Теги: `errors`.

Ссылка: https://yql.yandex-team.ru/Operations/XuIEjWim9YmO-YY6fV6G8XgulL86A2Qi0rhyItNDmD4=

```sql
use marketclickhouse;

select 
    *
from (
    select
        *
    from market.nginx2
    where 
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'   
) nginx

right join

(
    select
        request_id
    from market.market_errors
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and message like '%CartList%'
        and code = 'FailedViewError'
        and service like '%market_front_%'
) front_errors

on nginx.req_id = front_errors.request_id;
```
