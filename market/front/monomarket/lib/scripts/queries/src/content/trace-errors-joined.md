# JOIN трассировки и ошибок приложения

Позволяет отследить трассировки, на которых произошли ошибки. 

Помогает детально проанализировать причину возникновения ошибок в релизе.

Теги: `ошибки`, `трассировка`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbdDBJKfZcFhAEzJQxAFsv8OdABHUqXOb9GFR05dug=

```sql
USE marketclickhouse;

select
    target_module,
    request_method,
    code,
    count() as hits
from (
    select
        code,
        request_id,
        message,
        stack_trace,
        extra_keys,
        extra_values,
        substring(request_id, 1, 46) as trace_id
    from market.market_errors
    where date = toDate('2021-08-23')
    and timestamp >= toUnixTimestamp('2021-08-23 13:20:00')
    and timestamp <= toUnixTimestamp('2021-08-23 13:50:00')
    and environment = 'PRODUCTION'
    and service in ('market_front_api')
    and message = 'Timeout awaiting \'request\' for 1000ms'
    and host in (
        'man0-1821-0e6-man-market-prod-f-ba0-8041.gencfg-c.yandex.net',
        'man0-2161-man-market-prod-front-ba0-8041.gencfg-c.yandex.net',
        'vla3-1734-bb3-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
        'vla3-1742-969-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
    )
) as errors inner join (
    select
        id_ms,
        id_hash,
        type,
        target_module,
        request_method,
        http_code,
        query_params,
        kv_keys,
        kv_values,
        concat(toString(id_ms),  '/', id_hash) as trace_id
    from market.market_front_trace
    where date = toDate('2021-08-23')
    and timestamp >= toUnixTimestamp('2021-08-23 13:20:00')
    and timestamp <= toUnixTimestamp('2021-08-23 13:50:00')
    and environment = 'PRODUCTION'
    -- and target_module = ''
    -- and source_module = 'market_front_touch'
    and environment = 'PRODUCTION'
    and module = 'market_front_api'
    and host in (
        'man0-1821-0e6-man-market-prod-f-ba0-8041.gencfg-c.yandex.net',
        'man0-2161-man-market-prod-front-ba0-8041.gencfg-c.yandex.net',
        'vla3-1734-bb3-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
        'vla3-1742-969-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
    )
    and http_code != 200
) as trace
on errors.trace_id = trace.trace_id
group by target_module, request_method, code
order by hits desc;
```
