### MON_OIBA_CANCELLATION_DIVERGENCE

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_OIBA_CANCELLATION_DIVERGENCE&project=market-billing&last=1DAY)

Проверяет что cуммы по отменам услуг, не совпадают с суммами самих услуг (fee, доставка, loyalty, магистраль, экспрессы)

Критичность: критично для закрытия месяца.

Что делать: актуальные расхождения можно посмотреть по запросу
```sql
with services_with_cancellation as (
    select 'fee' as service, 'fee_cancellation' as cancellation
    union all
    select 'loyalty_participation_fee' as service, 'loyalty_participation_fee_cancellation' as cancellation
    union all
    select 'delivery_to_customer' as service, 'delivery_to_customer_cancellation' as cancellation
    union all
    select 'crossregional_delivery' as service, 'crossregional_delivery_cancellation' as cancellation
    union all
    select 'express_delivered' as service, 'express_delivered_cancellation' as cancellation
)
select fee.service_type, count(*) div_count, array_agg(cancel.item_id) items
from services_with_cancellation services
         join market_billing.order_item_billed_amounts cancel
              on services.cancellation = cancel.service_type
         join market_billing.order_item_billed_amounts fee
              on services.service = fee.service_type and cancel.item_id = fee.item_id
where cancel.trantime > current_date - 31 and cancel.amount + fee.amount <> 0
group by fee.service_type;
```
