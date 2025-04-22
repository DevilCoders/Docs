# OEBS/XXAP_AGENT_REWARD_DATA (ARD, agent reward data)

## О таблице

<https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA>

Великая и ужасная ARD.

Одна строчка -- одна транзакция

Записи отсюда потом обрабатываются программой подготовки пакетов и результат записывается в таблицу `agent_payment_batches`
(<https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_PAYMENT_BATCHES/MARKET/XXAP_AGENT_PAYMENT_BATCHES>)

Где происходит группировка: в момент попадения в ОЕБС, кажется.



## Немного вообще про ОЕБС

Контракт:
* номер договора `K_ALIAS`
* `K_NUMBER` -- `contract_id` в Биллинге
* `K_HEADER_ID` -- внутренний id договора в OEBS (в таблице `OKE_K_HEADERS` -- он же)

## Поля

### `LINE_ID (int64)`


### `BILLING_LINE_ID (int64)`

Идентификатор транзакции из Биллинга

### `DELETED_FLAG (string)`


### `PERIOD_END_DATE (string)`


### `ACTUAL_DATE (string)`


### `CUSTOMER_ID (int64)`


### `ROW_AMOUNT (double)`

Сумма строки

### `INITIAL_DATE (string)`


### `TRANSACTION_TYPE (string)`

Тип транзакции.

### `LOCAL_CURRENCY_CODE (string)`


### `ADDED_AMOUNT (double)`


### `AGENT_TYPE_CODE (string)`

Сервис (??)

### `K_HEADER_ID (int64)`


### `K_ALIAS (string)`

Номер договора

### `PAYSYS_TYPE_ID (int64)`

Дополнительный тип транзакции (или платежа?).
Например, может быть неттинг

### `PAYSYS_REWARD_AMT (double)`


### `PAYSYS_CURR_CODE (string)`


### `YANDEX_REWARD_AMT (double)`


### `LOCAL_ROW_AMOUNT (double)`


### `YANDEX_CURR_CODE (string)`


### `PAYMENT_AMOUNT (double)`


### `PAYMENT_CURR_CODE (string)`


### `FULLY_PAID_FLAG (string)`


### `PAYMENT_BATCH_ID (int64)`

id пакета, в рамках которого существует транзакция

### `PAID_AMOUNT (double)`


### `ORG_ID (int64)`

Организация Яндекса

### `CREATION_DATE (string)`


### `CREATED_BY (int64)`


### `LAST_UPDATE_DATE (string)`


### `LAST_UPDATED_BY (int64)`


### `LAST_UPDATE_LOGIN (int64)`


### `LINE_VERSION (int64)`


### `AGENT_TYPE_ID (int64)`


### `ACCOUNTING_DATE (string)`


### `COUNTRY_CODE (string)`


### `COUNTRY_SPECIFIC_ID (int64)`


### `PROCESS_STATUS (string)`


### `LINE_SOURCE (string)`


### `NETTING_BILL_NUMBER (string)`


### `PAYMENT_AUTHORIZE_DATE (string)`


### `ASSIGNED_K_HEADER_ID (int64)`


### `ACCRUAL_BATCH_ID (int64)`


### `SERVICE_ORDER_ID (string)`

* `'payment-order-%'` -- команды на выплату из Биллинга

### `TERMINAL_ID (int64)`


### `PAYMENT_CHECK_ID (int64)`


### `SERVICE_REFERENCE_ID (double)`


### `ORAROWID (string)`


