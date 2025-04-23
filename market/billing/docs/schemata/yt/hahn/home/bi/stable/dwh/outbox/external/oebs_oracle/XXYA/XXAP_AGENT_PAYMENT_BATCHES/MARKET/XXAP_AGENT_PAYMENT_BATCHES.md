# AGENT_PAYMENT_BATCHES

# О таблице

<https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_PAYMENT_BATCHES/MARKET/XXAP_AGENT_PAYMENT_BATCHES>

см. также [ARD](../../XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA.md)

Пакеты (батчи), агрегированная сущность OEBS.

Батч всегда по одному договору.

Пакетов по одному договору за один день может быть несколько.

Что ОЕБС делает с этой таблицей (это описание лучше вынести в "флоу выплат в OEBS", TODO):

По суммам в батчах определяем, есть ли положительная сумма к выплате.

Если сумма отрицательная: ОЕБС пишет в лог (`xxap_cpa_process_log`, доступна ли на YT?), что сумма отрицательная

TODO: `xxap_cpa_process_log` на YT есть, надо запросить права если их еще нет (Оля Т. советовала ее читать)


Если сумма положительная: создается запись в `xxap_draft_inoices` (драфтовая счет-фактура) по этому договору по этому пакету платежей.
TODO есть ли `draft_invoices` на YT?

Если реквизиты невалидные, то драфт-инвойс все равно создается, но остается необработанным (в драфт-инвойсе будет `amount_paid=0`, `payment_status_flag=N`)

## Релевантные ссылки

* <https://wiki.yandex-team.ru/users/ezhakenov/baza-znanijj.monetizacija/>


## Поля

### `BATCH_ID` (int64)


### `PROCESS_LINE_NUMBER` (int64)


### `ACTUAL_DATE` (string)


### `AGENT_TYPE_CODE` (string)


### `DOCUMENT_TYPE` (string)


### `DOCUMENT_ID` (int64)


### `DOCUMENT_NUMBER` (string)


### `CUSTOMER_ID` (int64)


### `VENDOR_ID` (int64)


### `VENDOR_SITE_ID` (int64)


### `K_HEADER_ID` (int64)


### `SUMMARY_ID` (int64)


### `DOCUMENT_DATE` (string)


### `PAYMENT_AMOUNT` (double)


### `TAX_AMOUNT` (double)


### `INV_CURRENCY_CODE` (string)


### `INV_CREATED_BY` (int64)


### `INV_CREATION_DATE` (string)


### `STATUS_CODE` (string)


### `RECONCILATION_DATE` (string)


### `RECONCILE_ACTION_DATE` (string)


### `RECONCILED_BY` (int64)


### `INVOICE_STATUS` (string)


### `RESULT_TEXT` (string)


### `PAYMENT_DETAILS` (string)


### `ORG_ID` (int64)


### `LAST_UPDATE_DATE` (string)


### `LAST_UPDATED_BY` (int64)


### `LAST_UPDATE_LOGIN` (int64)


### `EXT_BANK_ACCOUNT_ID` (int64)


### `COUNTRY_CODE` (string)


### `SERVICE_ID` (double)


### `REQUEST_ID` (int64)


### `REMIT_TO_SUPPLIER_SITE_ID` (int64)


### `SCHEDULED_PAYMENT` (string)


### `ORAROWID` (string)


