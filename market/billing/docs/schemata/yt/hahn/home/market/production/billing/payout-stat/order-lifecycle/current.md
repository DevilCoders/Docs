# Биллинг / payout-stat / order-lifecycle

<https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/payout-stat/order-lifecycle/latest>


## О таблице

Одна строчка в таблице -- это "товаро-платеж". Только "товар" -- это или товар, или доставка, а "платеж" -- это или платеж, или возврат платежа.

Строчка описывает, как выплата/удержание за этот товаро-платеж проезжает по "конвейеру выплат" и попадает к партнеру (выплачивается): когда проходит через примечательные стадии, сколько времени между ними проходит.

Поля `ts_*` -- дата-время прохождения разных стадий конвейера выплат.

Поля `days_*` -- количество дней между разными событиями; вычислены как разность соответствующих `ts_*` полей).

Ключ, которым идентифицируется сущность:

* `checkouter_id`
* `transaction_type`
* `entity_type`
* `entity_id`
* `product`
* `paysys_type_cc`

Генерируется джобой [{#T}](../../../../../../../../../reference/jobs/list/payoutLifecycleYtGeneratorExecutor.md)

## Поля

### `cnt` (int32)

Техническое поле, всегда равно 1, удобно использовать в DataLens, чтобы считать количество строчек в группе.

### `checkouter_id` (int64)

id платежа или рефанда

### `transaction_type` (string)

платеж или рефанд

### `entity_type` (string)

доставка или товар

### `entity_id` (int64)

id доставки или товара

### `product` (string)


### `paysys_type_cc` (string)


### `stage` (string)

Стейдж, в котором сейчас "находится" оплата

### `ts_order_created` (string)

Время создания заказа

### `ts_delivered` (string)

время доставки заказа

### `date_delivered` (string)

Дата доставки. По ней определяется, какое расписание выплат применять

### `ts_payout_created` (string)

время создания payout в Биллинге (это техническая промежуточная сущность, снаружи большого физического-финансового смысла не имеет)

### `ts_payment_order_created` (string)

время создания команды на выплату в Биллинге Маркета

### `ts_bank_order_created` (string)

время создания платежного поручения

### `payout_oferta_span_start` (string)

Начало "допуска по оферете": "когда ждать выплату".

### `payout_oferta_span_end` (string)

Конец "допуска по оферте": последний день, когда выплата еще укладывается в оферту.

### `days_delivered_to_bank_order_created` (int32)

Это и следующие поля `days_*` --  количество дней между разными событиями; вычислены как разность соответствующих `ts_*` полей.

### `days_payment_order_created_to_bank_order_created` (int32)


### `days_delivered_to_payment_order_created` (int32)


### `days_order_created_to_bank_order_created` (int32)


### `days_order_created_to_delivered` (int32)


### `days_delivered_to_payout_created` (int32)


### `days_payout_created_to_payment_order_created` (int32)


### `bank_order_id` (string)

Номер платежного поручения, в который вошла выплата

### `bank_order_sum` (int64)

Сумма платежного поручения

### `payment_type` (string)


### `service_order_id` (string)


### `trust_id` (string)


### `order_status` (utf8)


### `payout_sum` (int64)


### `partner_id` (int64)


### `contract_id` (int64)


### `payout_frequency` (utf8)

Тип расписания выплат: `"daily", "monthly", "bi-weekly", "weekly", "default"`

### `payment_order_id` (int64)


