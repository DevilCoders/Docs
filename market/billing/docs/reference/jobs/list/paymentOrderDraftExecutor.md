# PaymentOrderDraftExecutor

### Код

Основной код:

[класс PaymentOrderDraftExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderDraftExecutor.java)

[сервис PaymentOrderDraftService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PaymentOrderDraftService.java)

[дао PayoutDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/PayoutDao.java)

### Продукт/подсистема

Управление выплатами

### Роль в работе продукта/подсистемы

Джоба создает черновики (таблица market_billing.payment_order_draft) для команд на выплату.


### Датафлоу

Джоба считывает данные из таблиц [market_billing.payout](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/market_billing/payout.sql) и
[market_billing.payout_correction](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/market_billing/payout_correction.sql)
по условию `payout_group_id is null` и времени события `trantime < :date_to`. Далее она дообогащает эти данные информацией об id клиента и id контракта.
Группирует эти данные и либо обновляет записи в таблице
[market_billing.payment_order_draft](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/market_billing/payment_order_draft.sql)
либо вставляет новые. Данные обновляются/вставляются чанками по 10_000 штук за раз.


### Способы наблюдения за текущим состоянием
- Логи
- Изменения в базе


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




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

