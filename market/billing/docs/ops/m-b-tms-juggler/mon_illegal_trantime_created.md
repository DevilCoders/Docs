### MON_ILLEGAL_TRANTIME_CREATED

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_ILLEGAL_TRANTIME_CREATED&project=market-billing&last=1DAY)

Проверяет наличие трантаймов в таблице **_order_trantimes_** которых там не должно быть.

Критичность: критично для закрытия месяца.

Что делать: по этому запросу можно посмотреть хронологию статусов заказа и в какой момент появился нелегальный трантайм
```sql
with
    mbi_order_status as (
        select 'PROCESSING' as status_str, 0 as status
        union all
        select 'DELIVERY' as status_str, 1 as status
        union all
        select 'CANCELLED_IN_PROCESSING' as status_str, 2 as status
        union all
        select 'CANCELLED_IN_DELIVERY' as status_str, 3 as status
        union all
        select 'UNKNOWN' as status_str, 4 as status
        union all
        select 'DELIVERED' as status_str, 5 as status
        union all
        select 'PICKUP' as status_str, 6 as status
        union all
        select 'RESERVED' as status_str, 7 as status
        union all
        select 'UNPAID' as status_str, 8 as status
        union all
        select 'PENDING' as status_str, 9 as status
        union all
        select 'CANCELLED_BEFORE_PROCESSING' as status_str, 10 as status
    ),
    orders as (
        select order_id from market_billing.order_trantimes ot
        where ot.trantime >= current_date-31
          and not exists(
            select 1
            from market_billing.cpa_order_status_history cosh
            where ot.order_id = cosh.order_id and cosh.trantime > ot.trantime - interval '30' day
            )
    )
select order_id, trantime,
       'status_change' as type,
       (select status || ' - ' || status_str from mbi_order_status mis where mis.status = sh.status) status,
       '-' as service_type
from market_billing.cpa_order_status_history sh
where order_id in (select order_id from orders)
union all
select order_id, trantime, 'trantime_create' as type, '-' as status, service_type
from market_billing.order_trantimes
where order_id in (select order_id from orders)
order by order_id, trantime, type, service_type;
```
Cкорее всего, проблемные трантаймы - действительно лишние, и их нужно удалить миграцией и переобилить соответствующие услуги
