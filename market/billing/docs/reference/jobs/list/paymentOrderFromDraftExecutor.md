# PaymentOrderFromDraftExecutor

### Код

[джоба PaymentOrderFromDraftExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderFromDraftExecutor.java)

[сервис PaymentOrderFromDraftService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderFromDraftService.java)

[сервис PaymentOrderSchedulerService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderSchedulerService.java)

[дао PaymentOrderDraftDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/PaymentOrderDraftDao.java)

[дао PayoutScheduleDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/PayoutScheduleDao.java)


### Продукт/подсистема

Управление выплатами


### Роль в работе продукта/подсистемы

Создаёт команды на выплату партнёрам, используя предагрегированные данные из PaymentOrderDraft.


### Датафлоу

Джоба считывает данные из таблицы [market_billing.payout_schedule](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/payout_schedule.sql) для определения, по каким расписаниям должны быть выплаты в обрабатываемую дату, затем считывает данные из таблиц [market_billing.client_payout_frequency](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/client_payout_frequency.sql) и 
[market_billing.payment_order_draft](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/payment_order_draft.sql), получая данные необработанных черновиков команд для партнёров, которым необходимо произвести выплаты в обрабатываемую дату, по условию `processed = false` и время создания черновика `transaction_date < processing_date`. Далее джоба группирует эти данные по `contract_id`, `service_id`, `product`, `paysys_type_cc` и `currency`, фильтрует по минимальной сумме на выплату и сохраняет в таблицу [market_billing.payment_order](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/payment_order.sql), также сохраняет связь между командами на выплату и группами выплат в таблице [market_billing.payout_group_payment_order](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/payout_group_payment_order.sql) и обновляет обработанные черновики, проставляя им флаг `processed = true`. Данные о командах на выплату вставляются группами по 10 000 штук.


### Способы наблюдения за текущим состоянием
- Логи
- Изменения в базе
- Дата обработки в таблице [shops_web.environment](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/shops_web/environment.sql), ключ `market.billing.payment-order-from-draft-executor.date-to-collect`


### Какая функциональность пострадает от отказа джобы

Не будут происходить выплаты в сторону поставщиков.


### Как пользователи (или команда) заметят проблему и через какое время

Загорятся мониторы (здесь может быть ссылка на них).


### Контакты разработчиков и менеджеров

Разработчики: [Группа продуктовой разработки Биллинга Маркета](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_business_billing_dev_dep62586/) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

В течение дня надо устранить проблему.


### Способы регулирования работы джобы

Флаг `mbi.billing.payment.order.draft.enabled` в таблице [shops_web.environment](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/shops_web/environment.sql) позволяет переключить создание команд на выплату из черновиков (значение `true`) или напрямую из выплат (значение `false`).

Обрабатываемая дата `market.billing.payment-order-from-draft-executor.date-to-collect` в таблице [shops_web.environment](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/shops_web/environment.sql)


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

