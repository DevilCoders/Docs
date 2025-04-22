# Название джобы

### Код

[джоба DomesticPayoutFromAccrualExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/DomesticPayoutFromAccrualExecutor.java)

[сервис DomesticPayoutFromAccrualService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/DomesticPayoutFromAccrualService.java)


### Продукт/подсистема

Управление выплатами для внутреннего биллинга


### Роль в работе продукта/подсистемы

Создаёт записи про деньги, которые нужно выплатить или удержать у магазина.


### Датафлоу




### Способы наблюдения за текущим состоянием

- Логи
- Изменения в базе
- Juggler-проверки:


### Какая функциональность пострадает от отказа джобы

Не будут происходить выплаты в сторону поставщиков.


### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Группа продуктовой разработки Биллинга Маркета](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_business_billing_dev_dep62586/) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

В течение дня надо устранить проблему.


### Способы регулирования работы джобы

Флаг `market.billing.payout.from.accrual.domestic.enabled` в таблице [shops_web.environment](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/liquibase/shops_web/environment.sql) позволяет включить выполнение джобы (значение `true`).


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
