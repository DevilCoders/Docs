# disposalBillingExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/disposal/DisposalBillingExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/disposal/DisposalBillingService.java)
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/disposal/DisposalBillingDao.java)

### Продукт/подсистема
Обилливание утилизации поставок.

### Роль в работе продукта/подсистемы
Биллинг утилизации поставок на синем маркете. Услуга по организации утилизации Товаров включает в себя комплектацию,
упаковку и передачу Товара утилизирующей компании, а также взаимодействие с утилизирующей компанией.


### Датафлоу
Джоба запускается каждый час, начиная с 6:00, каждые два часа.
Обилливание смотрит на 2 источника данных - тарифы на выбранные даты и
 таблицу в бд `market_billing.fulfillment_supply_item`.


### Способы наблюдения за текущим состоянием
Juggler-мониторинг


### Какая функциональность пострадает от отказа джобы
Перестанет обилливаться утилизация



### Как пользователи (или команда) заметят проблему и через какое время
Juggler-мониторинг.


### Контакты разработчиков и менеджеров
Разработчик: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки
Ближайшие дни


### Способы регулирования работы джобы
* env-переменная с которой нужно обиллить: `market.billing.disposal_billing_executor.from_date`
* tms-команда для переобилливания: [DisposalBillingCommand](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/disposal/DisposalBillingCommand.java)

### Известные причины поломок


### Дополнительно: тонкости и подводные камни

