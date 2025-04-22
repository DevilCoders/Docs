# Чекаутер

На странице собрана некоторая полезная информация, которая может понадобиться при взаимодействии с Чекаутером.

## Подключение к БД { #db }

Инструкция, как подключаться к БД Чекаутера написано на wiki странице [Базы CPA бекэндов](https://wiki.yandex-team.ru/market/cpa/storage/).

## Tvm { #tvm }

При походе в ручки Чекаутера на проде, нужно в заголовке передавать сгенерированный tvm токен.
Как это сделать, написано на wiki странице [Получение доступа к ручкам, защищенным tvm](https://wiki.yandex-team.ru/market/marketplace/dev/sox/tvm-access/).

## SQL запросы { #sql }

### Получить все платежи по заказу { #payments-by-order-id }

{% cut "" %}

```sql
with order_ids as (
    select unnest(array [your_order_ids_separated_by_comma]) id
),
payment_by_order as (
    select p.order_id o_id, p.* from payment p where order_id in (select id from order_ids)
),
payment_by_order_payment as (
    select op.order_id o_id, p.*
    from payment p
             join order_payment op on p.id = op.payment_id
    where op.order_id in (select id from order_ids)
),
payment_by_payment_ids as (
    select o.id o_id, p.*
    from payment p
             join orders o on p.id = o.payment_id
    where o.id in (select id from order_ids)
),
all_payment as (
    select * from payment_by_order
    union
    select * from payment_by_order_payment
    union
    select * from payment_by_payment_ids
)
select * from all_payment
order by o_id;
```

{% endcut %}

### Получить все payment начисления по заказу { #payment-accrual-by-order-id }

{% cut "" %}

```sql
select p.id                                                                                       as payment_id,
       ri.order_id                                                                                as order_id,
       p.goal                                                                                     as payment_goal,
       ri.item_id                                                                                 as entity_id,
       'item'                                                                                     as entity_type,
       sum(case when r.type = 1 then -1 else 1 end * (ri.amount - coalesce(ri.yandex_cashback_amount, 0) - coalesce(ri.spasibo_amount, 0))) as amount,
       sum(case when r.type = 1 then -1 else 1 end * coalesce(ri.yandex_cashback_amount, 0))                                                as yandex_cashback_amount,
       sum(case when r.type = 1 then -1 else 1 end * coalesce(ri.spasibo_amount, 0))              as spasibo_amount,
--        ri.amount,
       o.fulfilment_shop_id                                                                       as partner_id,
       p.balance_service_id                                                                       as balance_service_id,
       p.status_updated_at                                                                        as p_status_updated_at
from payment as p
         join receipt as r on r.payment_id = p.id
         join receipt_item as ri on ri.receipt_id = r.id
         left join order_item as o on o.order_id = ri.order_id and o.id = ri.item_id
where ri.order_id = your_order_id
  and p.fake = false
  and p.mbi_control_enabled = true
  and p.status = 4                    -- CLEARED
  and p.goal in (0, 1, 2, 10, 12, 13, 15) -- ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION, ORDER_ACCOUNT_PAYMENT
  and ri.item_id is not null
  and r.type in (0, 1)                -- INCOME, INCOME_RETURN
  and r.status in (1, 50)             -- PRINTED, GENERATED
group by p.id, p.goal, ri.order_id, ri.item_id, ri.delivery_id, p.balance_service_id, p.status_updated_at,
         o.fulfilment_shop_id
union all -- delivery part
select distinct p.id                                                                                       as payment_id,
                ri.order_id                                                                                as order_id,
                p.goal                                                                                     as payment_goal,
                ri.order_id                                                                                as entity_id,
                'delivery'                                                                                 as entity_type,
                sum(case when r.type = 1 then -1 else 1 end * (ri.amount - coalesce(ri.yandex_cashback_amount, 0) - coalesce(ri.spasibo_amount, 0))) as amount,
                sum(case when r.type = 1 then -1 else 1 end * coalesce(ri.yandex_cashback_amount, 0))                                                as yandex_cashback_amount,
                sum(case when r.type = 1 then -1 else 1 end * coalesce(ri.spasibo_amount, 0))                                                        as spasibo_amount,
--                 ri.amount, ri.yandex_cashback_amount, ri.spasibo_amount,
                o.shop_id                                                                                  as partner_id,
                p.balance_service_id                                                                       as balance_service_id,
                p.status_updated_at                                                                        as p_status_updated_at
from payment as p
         join receipt as r on r.payment_id = p.id
         join receipt_item as ri on ri.receipt_id = r.id
         join orders as o on ri.order_id = o.id
where ri.order_id = your_order_id
  and p.fake = false
  and p.mbi_control_enabled = true
  and p.status = 4                    -- CLEARED
  and p.goal in (0, 1, 2, 10, 12, 13, 15) -- ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION, ORDER_ACCOUNT_PAYMENT
  and ri.delivery_id is not null
  and r.type in (0, 1)                -- INCOME, INCOME_RETURN
  and r.status in (1, 50)             -- PRINTED, GENERATED
group by p.id, p.goal, o.rgb, ri.order_id, p.balance_service_id, p.status_updated_at, o.shop_id;
```

{% endcut %}

### Получить все refund начисления по заказу { #refund-accrual-by-order-id }

{% cut "" %}

```sql
select p.id                                                                                     as payment_id,
       r.id                                                                                     as refund_id,
       ri.order_id                                                                              as order_id,
       p.goal                                                                                   as payment_goal,
       ri.item_id                                                                               as entity_id,
       'item'                                                                                   as entity_type,
       sum(ri.amount - coalesce(ri.yandex_cashback_amount, 0) - coalesce(ri.spasibo_amount, 0)) as amount,
       sum(coalesce(ri.yandex_cashback_amount, 0))                                              as yandex_cashback_amount,
       sum(coalesce(ri.spasibo_amount, 0))                                                      as spasibo_amount,
--        ri.amount,
       o.fulfilment_shop_id                                                                     as partner_id,
       p.balance_service_id                                                                     as balance_service_id,
       r.status_updated_at                                                                      as r_status_updated_at
from refund r
         join payment as p on p.id = r.payment_id
         join receipt as rc on rc.refund_id = r.id
         join receipt_item as ri on ri.receipt_id = rc.id
         left join order_item as o on o.order_id = ri.order_id and o.id = ri.item_id
where ri.order_id = your_order_id
  and p.fake = false
  and p.mbi_control_enabled = true
  and r.status = 1                    -- SUCCESS
  and p.goal in (0, 1, 2, 10, 12, 13, 15) -- ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION, ORDER_ACCOUNT_PAYMENT
  and ri.item_id is not null
  and rc.type = 1                     -- INCOME_RETURN
  and rc.status in (1, 50)            -- PRINTED, GENERATED
group by r.id, p.id, p.goal, ri.order_id, ri.item_id, ri.delivery_id, p.balance_service_id, p.status_updated_at,
         o.fulfilment_shop_id
union all -- delivery part
select distinct p.id                                                                                     as payment_id,
                r.id                                                                                     as refund_id,
                ri.order_id                                                                              as order_id,
                p.goal                                                                                   as payment_goal,
                ri.order_id                                                                              as entity_id,
                'delivery'                                                                               as entity_type,
                sum(ri.amount - coalesce(ri.yandex_cashback_amount, 0) - coalesce(ri.spasibo_amount, 0)) as amount,
                sum(coalesce(ri.yandex_cashback_amount, 0))                                              as yandex_cashback_amount,
                sum(coalesce(ri.spasibo_amount, 0))                                                      as spasibo_amount,
--                 ri.amount, ri.yandex_cashback_amount, ri.spasibo_amount,
                oi.fulfilment_shop_id                                                                    as partner_id,
                p.balance_service_id                                                                     as balance_service_id,
                r.status_updated_at                                                                      as r_status_updated_at
from refund r
         join payment as p on p.id = r.payment_id
         join receipt as rc on rc.refund_id = r.id
         join receipt_item as ri on ri.receipt_id = rc.id
         join order_item as oi on oi.order_id = ri.order_id
         join orders as o on oi.order_id = o.id
where ri.order_id = your_order_id
  and p.fake = false
  and p.mbi_control_enabled = true
  and r.status = 1                    -- SUCCESS
  and p.goal in (0, 1, 2, 10, 12, 13, 15) -- ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION, ORDER_ACCOUNT_PAYMENT
  and ri.delivery_id is not null
  and rc.type = 1                     -- INCOME_RETURN
  and rc.status in (1, 50)            -- PRINTED, GENERATED
group by r.id, p.id, p.goal, ri.order_id, p.balance_service_id, r.status_updated_at, oi.fulfilment_shop_id;
```

{% endcut %}

### Получить события по заказу в порядке публикации { #all_events-by-order-id }

{% cut "" %}

```sql
select
	o.id,
    oh.receipt_id,
    oe.event_id,
    mapeventtype(oe.event_type),
    o.created_at,
    oe.publish_time,
    maporderstatus(oh.status),
    mapordersubstatus(oh.substatus)
from orders o
         join order_history oh on oh.order_id = o.id
         join order_event oe  on oe.history_id = oh.id
where o.id in (:order_id)
order by o.id, oe.publish_time;
```

{% endcut %}

## Ссылки { #links }

- [{#T}](../reference/architecture/payment-control/payment-contract.md)
- wiki [Методы оплаты](https://wiki.yandex-team.ru/market/fintech/dokumentacija/metody-oplaty/)
- wiki с описанием нового топика по платежам/возвратам [PaymentEvents](https://wiki.yandex-team.ru/users/poluektov/paymentevents/)
