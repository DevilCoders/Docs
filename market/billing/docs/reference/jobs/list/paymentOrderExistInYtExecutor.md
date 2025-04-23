# paymentOrderExistInYtExecutor

### Код

[класс PaymentOrderExistInYtService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderExistInYtService.java)

[сервис PaymentOrderExistInYtService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderExistInYtService.java)

[дао PaymentOrderYtDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderYtDao.java)

[модель TotalPaymentOrder](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/TotalPaymentOrder.java)

### Продукт/подсистема

Управление выплатами

### Роль в работе продукта/подсистемы
Проверяется наличие команд на выплату 609 и 610 сервисов в тлогах в Ыте в таблицах `//home/market/production/billing/tlog/payouts/payments` `//home/market/production/billing/tlog/payouts/payments`

### Датафлоу

Джоба `paymentOrderExistInYtExecutor` запускается каждые полчаса начиная с 01:15 ночи и работает до 23:00 каждые полчаса.
Полезно отрабатывает первый раз, остальные запуски работают в холостую.

Происходит запрос в Ытевые таблицы тлогов(указаны ниже), который читает сумму команд на выплату (payments(610), expenses(609)) с типом [payment] за текущую дату(сегодня) по умолчанию.

Получившаяся сумма записывается в env с ключом `market.billing.tms.payment_order_total_sum_payments.<org_id>`
и `market.billing.tms.payment_order_total_sum_expenses.<org_id>`
(Здесь **<org_id>** отвечает за Операционную единицу, которая выполняет выплаты (локальный и глобальный маркет))

Время получения суммы с Ытя записывается в env с ключом `market.billing.tms.payment_order_total_sum.creation_time.<org_id>`.

На этом работа джобы заканчивается, и начинается работа моника `market_billing.mon_payment_order_exist`
и `market_billing.mon_payment_order_exist_global`

Команду на выплаты платежей(610) читает из пути `//home/market/production/billing/tlog/payouts/payments`
Команду на выплаты затрат(609) читает из пути `//home/market/production/billing/tlog/payouts/expenses`

Джоба полезно работает один раз, в остальное время работает в холостую.

### Способы наблюдения за текущим состоянием
_впиши актуальные ссылки_
- Juggler-проверки:
- Логи


### Какая функциональность пострадает от отказа джобы
Если не среагировать, то могут не выплатиться деньги поставщикам

### Как пользователи (или команда) заметят проблему и через какое время
1-Будет падать джоба `paymentOrderExistsInYtExecutor` в мониторе JOBS_PRIORITY_1.

2-Загорится монитор в УВ `mon_payment_order_exist_in_yt` и/или `mon_payment_order_exist_in_yt_global`.

3-Так как моники звонящие, робот позвонит дежурному.

### Контакты разработчиков и менеджеров

Разработчики: [adjanybekov](https://staff.yandex-team.ru/adjanybekov) <br/>
[rhrrd](https://staff.yandex-team.ru/rhrrd) <br/>
[a-kolchanov](https://staff.yandex-team.ru/a-kolchanov) <br/>

Менеджеры: [a-kolchanov](https://staff.yandex-team.ru/a-kolchanov)


### Желательное время исправления в случае поломки




### Способы регулирования работы джобы
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



4-И в конце **PaymentOrderExistInYtExecutor**

Считывает записи с тлоговых таблиц в Ыте с 01:05 до 2:00 каждые 15 минут.
Полезно отрабатывает первый раз, остальные запуски работают в холостую.

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
                 and org_id in (64554L, 6599577L)
                 UNION all
                 SELECT
                    org_id, service_id, cast (nvl(amount, "0") as double) as amount
                 FROM `//home/market/production/billing/tlog/payouts/payments/2022-03-08`
                 where service_id=610 and record_type='payment'
                 and org_id in (64554L, 6599577L)
        ) group by org_id, service_id)
    group by service_id, org_id, total_amount)
group by org_id;
```
И сумму тлогов кладет в энвайрмент ПГ по ключу _market.billing.tms.payment_order_total_sum_payments.<org_id>_ и _market.billing.tms.payment_order_total_sum_expenses.<org_id>_
```sql
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_payments.<org_id>';
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum_expenses.<org_id>';
```
И время записи по ключу _market.billing.tms.payment_order_total_sum.creation_time.<org_id>_
```sql
select * from shops_web.environment where name = 'market.billing.tms.payment_order_total_sum.creation_time.<org_id>';
```
<org_id> можно взять из класса OperatingUnit. На момент написание доки их два: 64554, 6599577.
### Известные причины поломок




### Дополнительно: тонкости и подводные камни
