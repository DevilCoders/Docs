# CancelledOrderAccrualExecutor

### Код

Основной код:

[сервис CancelledOrderAccrualService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/CancelledOrderAccrualService.kt)

[класс CancelledOrderAccrualExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/CancelledOrderAccrualExecutor.kt)

### Продукт/подсистема

Управление выплатами

### Роль в работе продукта/подсистемы

Джоба отменяет начисления (accrual) для отменённых заказов.
Для этого начислениям, которые соответствуют отменённым заказам, устанавливается статус платежа `payout_status = cancelled`


### Датафлоу

Джоба считывает данные из таблиц [market_billing.accrual](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/accrual.sql), [market_billing.cpa_order](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/cpa_order.sql) и
[market_billing.order_payout_trantime](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_payout_trantime.sql)
по условию `payout_status = new` и статусу заказа `Отменён` (7 или 9) и отсутствия записи в order_payout_trantime.
После этого у записей в `market_billing.accrual` устанавливается статус `payout_status = cancelled`.


### Способы наблюдения за текущим состоянием
- Логи
- Изменения в базе


### Какая функциональность пострадает от отказа джобы

Будут накапливаться начисления для отменённых заказов


### Как пользователи (или команда) заметят проблему и через какое время

TODO


### Контакты разработчиков и менеджеров

Разработчики: [Группа продуктовой разработки Биллинга Маркета](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_business_billing_dev_dep62586/) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

В течение дня надо устранить проблему.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

