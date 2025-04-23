# Закрытие месяца в международном биллинге (Израиль)

## Короткий путь проверок

1. Для проверки, что все джобы отработали до текущей даты [bill-global-completeness.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/bill-global-completeness.sh)
2. Для услуг запустит скрипт [tlog-global-collected.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/tlog-global-collected.sh)
3. Для УВ запустить скрипт [global-payment-control.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/global-payment-control.sh)

Ниже более детальные проверки, могут быть полезными, если нашлись расхождения.

## Услуги

### Global_fee
- проверить историю работы джобы [globalOrderFeeBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/GlobalOrderFeeBillingExecutor.java?rev=r9255581#L14)
- проверить что для всех записей в таблице трантаймов есть обилленые значения:
```sql
  select * from market_billing.global_order_trantime got
  left join market_billing.global_order_item_billed_amount goiba on goiba.order_id = got.order_id
  where got.service_type = 'global_fee'
  and got.trantime >= :date_from
  and got.trantime < :date_to
  and goiba.order_id is null;
```
  Если есть необилленые записи, то нужно перебиллить с начала месяца.
  Если есть ошибочные айтемы, которые ломают обилливание, то можно написать в чатик международки - https://t.me/joinchat/TqaCGuZu83MxY2Qy и если таких заказов мало, то заигнорить ломающие обилливание айтемы.

### Global_delivery
- проверить историю работы джобы [GlobalOrderDeliveryBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/GlobalOrderDeliveryBillingExecutor.java?rev=r9255581#L14)
```sql
  select * from market_billing.global_order_trantime got
  left join market_billing.global_order_billed_amount goba on goba.order_id = got.order_id
  where got.service_type = 'global_delivery'
  and got.trantime >= :date_from
  and got.trantime < :date_to
  and goba.order_id is null;
  ```
- Если есть необилленые записи, то надо перебиллить с начала месяца.

### Global_agency_commission
- обилливание идет по акруалам, трантаймы не используются
- проверить историю работы джобы [GlobalAgencyCommissionBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/agency/commission/GlobalAgencyCommissionBillingExecutor.java?rev=r9255581#L14)
```sql
  select * from market_billing.accrual acc
  left join market_billing.global_agency_comm_billed_amount gacba on gacba.entity_id = acc.entity_id
  where acc.org_id = 6599577
  and acc.trantime >= :date_from
  and acc.trantime < :date_to
  and gacba.entity_id is null;
```

## УВ
Лучше смотреть по мониторингам:
<br>mon_global_accrual_trantimes_created - создание трантаймов на начисления
<br>mon_global_accrual_created - создание акруалов
<br>mon_global_payout_created - создание начислений для выплаты
<br>mon_absent_global_contract - проверяет наличие договоров для международных магазинов
<br>mon_global_payment_order_created - создание команд на выплату
<br>mon_global_payment_orders_for_today - создаются команды на выплату за сегодня
<br>mon_payment_order_exist_in_yt_global - команды на выплату создались в YT mon_payment_order_exist_in_yt_global
