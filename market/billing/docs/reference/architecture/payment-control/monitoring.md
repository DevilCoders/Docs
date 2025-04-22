# Мониторинги и сверки

## Мониторинги

### MON_BANK_ORDER_SYNC

[Juggler](https://juggler.yandex-team.ru/project/market-billing/aggregate?host=market-billing&service=MON_BANK_ORDER_SYNC&project=market-billing)


Проверяет, что нет расхождения общей суммы ПП с суммами по детализации


Что делать: Надо найти paymentBatchId платежных поручений, для которых сумма в заголовке ПП (market_billing.bank_order) отличается от суммы детализации (market_billing.bank_order_item). Например, таким запросом
```
select bo.PAYMENT_BATCH_ID
from market_billing.bank_order_item boi
         join MARKET_BILLING.bank_order bo on bo.payment_batch_id = boi.payment_batch_id
where bo.trantime >= date(current_timestamp) - 90 --дата, на которую смотрит монитор, можно убрать
group by bo.SUM, bo.payment_batch_id
having sum(case when boi.transaction_type = 'payment' then boi.sum else -boi.sum end) <> bo.sum
```

Далее можно воспользоваться командой **delete-bank-order-item**, которая удалит детализацию по указанным paymentBatchId. Затем надо запустить **BankOrderItemsImportExecutor**, который импортирует детализацию из Баланса для всех ПП, для которых нет детализации.



### MON_PAYMENT_ORDER

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_ORDER&project=market-billing&last=1DAY)

Проверяет, что в Postgres в таблице market_billing.payment_order есть записи для Синего Маркета за сегодняшний день.

Критичность: always_crit.

Что делать:


### MON_GLOBAL_PAYMENT_ORDER

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_GLOBAL_PAYMENT_ORDER&project=market-billing&last=1DAY)

Проверяет, что в Postgres в таблице market_billing.payment_order есть записи для Международного Маркета за сегодняшний день.

Критичность: выплаты происходят в понедельник для 610 сервиса и во вторник для 609 сервиса (расписание хранится в OEBS). Критично в понедельник, вторник и пятницу.

Что делать:

### mbi-billing-2902

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-2902&project=market.common&last=1DAY)

> Пример ошибки: Number of unprocessed accrual_trantimes: 10, number of unprocessed refund_trantimes: 53

Проверяет наличие необработанных accrual_trantimes.

Критичность: критично, если количество превышает порог. Влияет на создание начислений и выплат. Критично при закрытии месяца.

Что делать:

### MON_PAYOUT_WITHOUT_PAYMENT_ORDER_DRAFT

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-2902&project=market.common&last=1DAY)

> Пример ошибки: There are 427 payouts without payment order draft (market-billing)

Проверяет наличие payout, которые не собрались в драфты (и не будут выплачены магазинам).

Критичность: критично, если количество превышает порог.

Что делать:

### MON_PAYMENT_CONTROL_TLOG_COLLECTION

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_CONTROL_TLOG_COLLECTION&project=market-billing&last=1DAY)

Критичность:

Что делать:


### MON_PAYMENTS_PAYMENT_CONTROL_TLOG_EXPORT

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENTS_PAYMENT_CONTROL_TLOG_EXPORT&project=market-billing&last=1DAY)

Критичность:

Что делать:


### MON_EXPENSES_PAYMENT_CONTROL_TLOG_EXPORT

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_EXPENSES_PAYMENT_CONTROL_TLOG_EXPORT&project=market-billing&last=1DAY)

Критичность:

Что делать:
Что делать:

### mbi-billing-2943

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-2923&project=market.common&last=1DAY)

Критичность:

Что делать: см. [документацию](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/2943/)

### MON_PAYMENT_DRAFT_PAYMENT_ORDER_AMOUNT_MATCH

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_DRAFT_PAYMENT_ORDER_AMOUNT_MATCH&project=market-billing&last=1DAY)

Критичность:

Что делать:

### MON_PAYMENT_DRAFT_PAYOUT_AMOUNT_MATCH

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_DRAFT_PAYOUT_AMOUNT_MATCH&project=market-billing&last=1DAY)

Критичность:

Что делать:

### MON_PAYMENT_PAYOUT_AMOUNT_MATCH

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_PAYOUT_AMOUNT_MATCH&project=market-billing&last=1DAY)

Критичность:

Что делать:

### MON_GLOBAL_ACCRUAL_TRANTIME_CREATED

Проверяет создание трантаймов на начисления в таблицу market_billing.global_accrual_trantime во время импорта международных заказов.

Критичность: критично, без этого не будет созданы начисления и не пройдут выплаты партнерам

Что делать: первым делом проверить импорт заказов, если они создаются, а в таблице market_billing.global_accrual_trantime пусто - возможно были изменения в коде джобы импорта или в схеме таблицы.
Джоба импорта - [GlobalOrderImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderImportExecutor.java?rev=r9255581#L17)

### MON_GLOBAL_ACCRUAL_CREATED

Проверяет, что обрабатываются трантаймы по начислениям  международного биллинга (Израиль).

Критичность: критично, если загорается, то значит мы не создаем начисления по международным заказам

Что делать: проверить джобу создания начислений по записям в таблице market_billing.global_accrual_trantime [GlobalAccrualTrantimesProcessingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/GlobalAccrualTrantimesProcessingExecutor.java?rev=r9315835#L21)

### MON_GLOBAL_PAYOUT_CREATED

Проверяет создание выплат по начислениям.

Критичность: критично, не будет выплат партнерам

Что делать: проверить работу джобы [globalPayoutFromAccrualExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/config/payment/PaymentConfig.java?rev=r9286458#L298)

### MON_GLOBAL_PARTNER_CONTRACT_CREATED

Проверка заведенности договоров по международным партнерам.

Критичность: очень критично! особенно для закрытия месяца - не соберем обилленые значения и выплаты, те без договоров магазин ничего не получит вовсе.

Что делать: идти к Саше Швецу @ashwets или в чатик международки https://t.me/joinchat/TqaCGuZu83MxY2Qy и сообщить номер(а) магазинов.

### MON_GLOBAL_PAYMENT_ORDER_CREATED

Проверка создания команд на выплату по драфтам

Критичность: критично для партнеров, если не будет команд, то выплата будет задержана.

Что делать: проверить какие драфты не выплачены, убедиться, что дата драфтов и начислений в прошедшем числе, иначе можно задаунтаймить монитор до завтра (выплаты каждый день идут по Изралию).

### MON_GLOBAL_TRANTIME_CREATED

Проверяет создание трантаймов на услуги (fee, delivery).

Критичность: очень критично, значит скорее всего что у нас ошибки в импорте заказов

Что делать: смотреть запуски джобы [GlobalOrderImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderImportExecutor.java?rev=r9255581#L17)
и её код

### MON_GLOBAL_BILLED_RECORDS_COLLECTED

Проверка сбора обилленых значений в тлог.

Критичность: критично для закрытия месяца.

Что делать: смотреть в первую очередь причину падения джобы сбора в тлог [TransactionLogCollectionExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/executor/TransactionLogCollectionExecutor.java?rev=r9255581#L17)
Возможно стоит проверить наличие  контрактов для поставщиков по мониторингу MON_GLOBAL_PARTNER_CONTRACT_CREATED

### MON_GLOBAL_FEE_BILLED

Проверяем, что обиллили все заказы по международке по услуге global_fee.

Критичность: критично для закрытия месяца.

Что делать: смотреть результат работы джобы [GlobalOrderFeeBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/GlobalOrderFeeBillingExecutor.java?rev=r9255581#L14)
Возможно поможет перебилливание месяца, если заказы приезжают из ытя позже  обилливания.

### MON_GLOBAL_DELIVERY_BILLED

Проверяем, что обиллили все заказы по международке по услуге global_delivery.

Критичность: критично для закрытия месяца.

Что делать: смотреть результаты джобы [GlobalOrderDeliveryBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/GlobalOrderDeliveryBillingExecutor.java?rev=r9255581#L24)
Аналогично global_fee можно попробовать перебиллить месяц с начала, проверить расписания импорта/обилливания.

### MON_GLOBAL_AGENCY_COMM_BILLED

Проверяем, что обиллили все заказы по международке по услуге global_agency_commission.

Критичность: критично для закрытия месяца.

Что делать: смотреть результаты джобы [GlobalAgencyCommissionBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/agency/commission/GlobalAgencyCommissionBillingExecutor.java?rev=r9255581#L14)
Аналогично global_fee можно попробовать перебиллить месяц с начала, проверить расписания импорта/обилливания.
Проверить что есть договоры в таблице market_billing.global_partner_contract

### MON_PAYMENT_ORDER_EXIST_IN_YT

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_ORDER_EXIST_IN_YT&project=market-billing&last=1DAY)

Проверяет, наличие команд на выплату расходных и доходных(609 и 610) сервисов в тлогах в Ыте для операционной единицы в РФ (org_id = 64554).
Наличием команд на выплату считается сумма команд на выплату больше лимита (на момент написания доки больше 100_000 рублей)

Если до 1.30 (по Москве) в Ытевой таблице(в запросе ниже) не сформировались Команды на Выплату, то моник звонит дежурному.

Критичность: always_crit.

Что делать:
Надо посмотреть флоу описанный ниже. Найти и решать шаг который дал сбой.

1-Сначала **PaymentOrderFromDraftExecutor** формирует команду на выплаты

Каждый час начиная с 00.30 (1.30, 2.30)

И записывает в таблицу **market_billing.payment_order**



2-Потом **PayoutsTransactionLogCollectionExecutor**  берет из таблицы payment_order и кладет в тлог

Каждые 15 минут начиная с 00.00 (00.15, 00.30, 00.45)

расходные в **market_billing.expenses_payouts_transaction_log**

доходные в **market_billing.payments_payouts_transaction_log**



3-Затем **PaymentsPayoutsTransactionLogYtExportExecutor** перекладывает тлоги из ПГ в Ыть

Работает каждые полчаса с 00.00 (00.30, 01.00)

_//home/market/production/billing/tlog/payouts/payments_

_//home/market/production/billing/tlog/payouts/expenses_



4-И в конце **PaymentOrderExistInYtService**

Считывает записи с тлоговых таблиц в Ыте каждые 15 минут начиная с 1:05 до 2:00

Запрос выглядит так **(даты надо поставить актуальные)**
``` sql
Use hahn;

select org_id, sum(sum609) as sum609, sum(sum610) as sum610 from (
    select org_id,
        case
            when service_id = 609
            then total_amount
        else 0 end
        as sum609,
        case
            when service_id = 610
            then total_amount
        else 0 end
        as sum610
    from(
        select org_id, service_id, nvl(sum(amount), 0) as total_amount
        from (
                 SELECT
                     org_id, service_id, cast (nvl(amount, "0") as double) as amount
                 FROM `//home/market/production/billing/tlog/payouts/expenses/2022-03-08`
                 where service_id=609 and record_type='payment'
                 and org_id = 64554L
                 UNION all
                 SELECT
                    org_id, service_id, cast (nvl(amount, "0") as double) as amount
                 FROM `//home/market/production/billing/tlog/payouts/payments/2022-03-08`
                 where service_id=610 and record_type='payment'
                 and org_id = 64554L
        ) group by org_id, service_id)
    group by service_id, org_id, total_amount)
group by org_id;
```
И сумму тлогов кладет в энвайрмент ПГ по ключу _market.billing.tms.payment_order_total_sum_payments.64554_ и _market.billing.tms.payment_order_total_sum_expenses.64554_
```sql
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_payments.64554';
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_expenses.64554';
```
И время записи по ключу _market.billing.tms.payment_order_total_sum.creation_time.64554_
```sql
select * from shops_web.environment where name= 'market.billing.tms.payment_order_total_sum.creation_time.64554';
```
А также если, моник погашен вручную, то в environment ставится флажок: TRUE по ключу _market.billing.tms.payment_order_total_sum.ok.64554.<current_date>_
```bash
env set market.billing.tms.payment_order_total_sum.ok.64554.2022-03-08 true
```
### MON_PAYMENT_ORDER_EXIST_IN_YT_GLOBAL

[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_PAYMENT_ORDER_EXIST_IN_YT_GLOBAL&project=market-billing&last=1DAY)

Проверяет, наличие команд на выплату расходных и доходных(609 и 610) сервисов в тлогах в Ыте для операционной единицы в Израиле (org_id = 6599577)
Наличием команд на выплату считается сумма команд на выплату больше лимита (на момент написания доки больше 0 рублей)

Если до 1.30 (по Москве) в Ытевой таблице(в запросе ниже) не сформировались Команды на Выплату, то моник звонит дежурному.

Критичность: always_crit.

Что делать:
Надо посмотреть флоу описанный ниже. Найти и решать шаг который дал сбой.

1-Сначала **PaymentOrderFromDraftExecutor** формирует команду на выплаты

Каждый час начиная с 00.30 (1.30, 2.30)

И записывает в таблицу **market_billing.payment_order**



2-Потом **PayoutsTransactionLogCollectionExecutor**  берет из таблицы payment_order и кладет в тлог

Каждые 15 минут начиная с 00.00 (00.15, 00.30, 00.45)

расходные в **market_billing.expenses_payouts_transaction_log**

доходные в **market_billing.payments_payouts_transaction_log**



3-Затем **PaymentsPayoutsTransactionLogYtExportExecutor** перекладывает тлоги из ПГ в Ыть

Работает каждые полчаса с 00.00 (00.30, 01.00)

_//home/market/production/billing/tlog/payouts/payments_

_//home/market/production/billing/tlog/payouts/expenses_



4-И в конце **PaymentOrderExistInYtService**

Считывает записи с тлоговых таблиц в Ыте каждые 15 минут начиная с 1:05 до 2:00
Запрос выглядит так **(даты надо поставить актуальные)**
``` sql
Use hahn;

select org_id, sum(sum609) as sum609, sum(sum610) as sum610 from (
    select org_id,
        case
            when service_id = 609
            then total_amount
        else 0 end
        as sum609,
        case
            when service_id = 610
            then total_amount
        else 0 end
        as sum610
    from(
        select org_id, service_id, nvl(sum(amount), 0) as total_amount
        from (
                 SELECT
                     org_id, service_id, cast (nvl(amount, "0") as double) as amount
                 FROM `//home/market/production/billing/tlog/payouts/expenses/2022-03-08`
                 where service_id=609 and record_type='payment'
                 and org_id = 6599577L
                 UNION all
                 SELECT
                    org_id, service_id, cast (nvl(amount, "0") as double) as amount
                 FROM `//home/market/production/billing/tlog/payouts/payments/2022-03-08`
                 where service_id=610 and record_type='payment'
                 and org_id = 6599577L
        ) group by org_id, service_id)
    group by service_id, org_id, total_amount)
group by org_id;
```

И сумму тлогов кладет в энвайрмент ПГ по ключу _market.billing.tms.payment_order_total_sum.6599577_ и _market.billing.tms.payment_order_total_sum_expenses.6599577_
```sql
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_payments.6599577';
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_expenses.6599577';
```
И время записи по ключу _market.billing.tms.payment_order_total_sum.creation_time.6599577_
```sql
select * from shops_web.environment where name= 'market.billing.tms.payment_order_total_sum.creation_time.6599577';
```
А также если, моник погашен вручную, то в environment ставится флажок: TRUE по ключу _market.billing.tms.payment_order_total_sum.ok.6599577.<current_date>_
```bash
env set market.billing.tms.payment_order_total_sum.ok.6599577.2022-03-08 true
```

## Сверки

### Сверки Checkouter - Market Billing

Для каждого платежа есть 4 сверки: платеж в Checkouter - начисление в MB, рефанд в Checkouter - начисление в MB, платеж в Checkouter - выплата в MB, рефанд в Checkouter - выплата в MB.

> Горящие сверки блокируют корректное закрытие месяца.

Посмотреть текущее состояние сверок можно на [Дашборде Juggler](https://juggler.yandex-team.ru/dashboards/market-billing/).

|Способ оплаты (goal)|Начисление платёж|Начисление рефанд|Выплата платёж|Выплата рефанд|
|----------|:-------------:|------:|:-------------:|------:|
| Предоплата(0)|  || ||
| субсидия(1)|  || ||
| постоплата(2)|  || ||
| tinkoff credit(10)|  || ||
| bnpl(12)|  || ||
| Общая сверка|  || ||

### Сверки Market Billing - ARD

### Сверки Checkouter - ARD
