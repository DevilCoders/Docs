# Админка платежей: анализ существующих ручек

## Общие для большинства ручек базы и сервисы

db.orders (нужен write access)
db.order_proc (нужен write access)
db.finance_tickets_zendesk (нужен write access)
db.corp_clients (нужен write access)

archive-api
chatterbox
startrack
stq (update_transactions, corp_sync_order и другие задачи)
territories

Также используются различные конфиги (TODO: список)

## Общая оценка работ


## Ручки (готово)

### /api/payments/orders_info/

**Код**: `taxiadmin.api.views.payments.get_orders_info`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** ~2w (минимум)

#### Зависимости

Пермишн `view_orders_limited` больше не выдаётся, его можно удалять,
 заменив на фильтр `countries_filter` в эксперименте `admin_restrictions`.
Пермишн `accept_card_orders`.
Дополнительный пермишн `search_by_user_phone` при поиске по телефону.


#### Внешние сервисы и базы

Берёт заказы из db.orders + archive-api (по id, phone_id, billing_id карт)
При поиске по номеру телефона получает phone_id из user-api
При поиске по карте ходит в db.users, ищет по yandex_uid (полученному из cardstorage).
 Нужно проверить, можно ли такие же данные получить из user-api.

При поиске по тикету ходит в db.finance_tickets_zendesk

Для получения доп. данных ходит в коллекции:
 db.dbdrivers, db.parks, db.subventions, db.users, db.user_phones,
 db.tariff_settings, db.order_proc, db.unique_drivers,

Также ходит в сервисы cardstorage, territories

### /api/payments/{order_id}/ 

**Код**: `taxiadmin.api.views.payments.get_fiscal_receipt_urls`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1d 

#### Зависимости

Пермишн `view_order_payments`.

#### Внешние сервисы и базы

db.orders

archive-api

### /api/payments/accept/, /api/payments/decline/

**Код**: `taxiadmin.api.views.payments.accept`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** ~1w на обе ручки (используют один код с разными аргументами)

#### Зависимости

Пермишн `accept_card_orders_full`
Аудит-экшны `payments_accept` и `payments_decline`.

#### Внешние сервисы и базы

см. общие

### /api/payments/move_to_cash/ 

**Код**: `taxiadmin.api.views.payments.move_to_cash`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1-2d

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `payments_move_to_cash`.

#### Внешние сервисы и базы (помимо общих)

db.promocode_series

cardstorage

stq (debts_processing)

### /api/payments/back_to_card/ 

**Код**: `taxiadmin.api.views.payments.back_to_card`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1-2d

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `payments_back_to_card`.

#### Внешние сервисы и базы

см. общие

### /api/payments/reason_codes/, /api/payments/new_sum_reason_codes/

**Код**:
    `taxiadmin.api.views.payments.get_reason_codes`
    `taxiadmin.api.views.payments.get_new_sum_reason_codes`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1d

#### Зависимости

Пермишн `accept_card_orders`.

#### Внешние сервисы и базы

Только переводы из localizations.

Отдают статичные данные из кода.

### /api/payments/compensation_reasons/

**Код**: `taxiadmin.api.views.payments.get_compensation_reasons`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1d вместе с `reason_codes`

#### Зависимости

Пермишн `accept_card_orders`.

#### Внешние сервисы и базы

Только переводы из localizations.

Отдаёт данные из конфига.

### /api/payments/update_order_ride_sum_to_pay/ + 2 похожие ручки

**Код**:
 `taxiadmin.api.views.payments.update_order_ride_sum_to_pay`
 `taxiadmin.api.views.payments.update_order_driver_ride_sum_to_pay`
 `taxiadmin.api.views.payments.update_order_decoupling_ride_sum_to_pay`

Часть кода общая.

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1w на три ручки (если есть быстрое решение для замены db.cities)

#### Зависимости

Пермишн `accept_card_orders_full`
 (также `payments_ignore_max_sum` для сумм больше лимита и `charge_users` для списаний).
Аудит-экшн `payments_update_sum_to_pay` (также `payments_ignore_max_sum`).

#### Внешние сервисы и базы

db.cities (для получения лимитов из поля `card_payment_settings`)
db.tariff_settings

cardstorage
stq (change_claim_order_price, corp_refund)

### /api/payments/compensate_park/ 

**Код**: `taxiadmin.api.views.payments.compensate_park`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1w (возможно, больше, надо смотреть детальнее)

#### Зависимости

Пермишн `payments_compensate_park` + один из двух:
 `compensate_park_via_subventions`/`accept_card_orders_full`.
 Также может проверяться `payments_ignore_max_sum`.

Аудит-экшн `payments_compensate_park`.

#### Внешние сервисы и базы (кроме общих)

db.parks
db.cities
db.tariff_settings

stq (update_transactions)
transactions

Возможно, какие-то ещё, детально не смотрел.

### /api/payments/refund_compensation/ 

**Код**: `taxiadmin.api.views.payments.refund_compensation`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 3-4d, может быть 1w (много нового кода)

#### Зависимости

Пермишн `refund_compensations`.
Аудит-экшн `payments_refund_compensation`.

#### Внешние сервисы и базы

stq (billing_process_payments)
transactions

Возможно, какие-то ещё, детально не смотрел.

### /api/payments/rebill_order/ 

**Код**: `taxiadmin.api.views.payments.rebill_order`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 2-3d

#### Зависимости

Пермишн `rebill_orders`.
Аудит-экшн `rebill_order`.

#### Внешние сервисы и базы

db.orders
db.order_proc

billing-orders

### /api/payments/refresh/ 

**Код**: `taxiadmin.api.views.payments.refresh`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 2d

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `payments_refresh`.

#### Внешние сервисы и базы

db.orders

stq (update_transactions)

### /api/payments/move_from_expired/ 

**Код**: `taxiadmin.api.views.payments.move_from_expired`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 2d

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `payments_move_from_expired`.

#### Внешние сервисы и базы (помимо общих)

db.closed_expired_orders

stq (move_from_expired_to_finished)

### /api/payments/dispatch/ 

**Код**: `taxiadmin.api.views.payments.accept_or_decline_dispatch`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 3-4d

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `payments_accept_or_decline_dispatch`.

#### Внешние сервисы и базы (кроме общих)

db.tariffs

stq (prepare_order_event)

Возможно, что-то ещё, надо смотреть детальнее

### /api/payments/dispatch_new_ride_sum_to_pay/ 

**Код**: `taxiadmin.api.views.payments.dispatch_new_ride_sum_to_pay`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 3d (можно делать одновременно с /api/payments/dispatch/ — много общего кода)

#### Зависимости

Пермишн `accept_card_orders_full`.
Аудит-экшн `manualaccept`.

#### Внешние сервисы и базы

См. /api/payments/dispatch/

### /api/payments/unbind_zendesk_ticket/ 

**Код**: `taxiadmin.api.views.payments.unbind_zendesk_ticket`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 1d

#### Зависимости

Пермишн `accept_unbind_zendesk_ticket`.
Аудит-экшн `unbind_ticket`.

#### Внешние сервисы и базы

db.finance_tickets_zendesk и часть общих (для проверок тикетов)

### /api/payments/lock_reasons/ 

**Код**: `taxiadmin.api.views.cardlocks.get_lock_reasons`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 3-4d

#### Зависимости

Пермишн `view_cardlock_reasons`.

#### Внешние сервисы и базы

db.orders
db.users
db.user_phones
db.phonelocks
db.devicelocks
db.cardlocks

user-api
cardstorage
archive-api

### /api/payments/unmark_debtor/ 

**Код**: `taxiadmin.api.views.payments.unmark_user_as_debtor`

**YAML:** Есть, актуальность не проверялась.

**Оценка:** 3d

#### Зависимости

Пермишн `unmark_user_as_debtor`.
Аудит-экшн `unmark_user_as_debtor`.

#### Внешние сервисы и базы

db.orders
db.users
db.phonelocks
db.devicelocks
db.cardlocks

archive-api
cardstorage
stq (debts_processing)
