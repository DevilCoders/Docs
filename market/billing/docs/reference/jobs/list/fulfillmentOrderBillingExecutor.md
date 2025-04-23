# fulfillmentOrderBillingExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentOrderBillingExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentOrderBillingService.java).

### Продукт/подсистема
Биллинг синих заказов

### Роль в работе продукта/подсистемы
Осуществляет биллинг синих заказов, для дальнейшей отгрузки в тлог, а следом в баланс.

### Датафлоу
Джоба запускается каждый полчаса с 00:15. Работает со схемой `market_billing` Собирает заказы из `trantimes`, по ним ищет данные в
`cpa_order` и `cpa_order_item`, вместе с промоакциями и тарифами ведет обработку и записывает данные в `order_item_billed_amounts`.


### Способы наблюдения за текущим состоянием
Juggler.


### Какая функциональность пострадает от отказа джобы
Вся система обилливания данных.


### Как пользователи (или команда) заметят проблему и через какое время
По мониторингу


### Контакты разработчиков и менеджеров



### Желательное время исправления в случае поломки
Чем быстрее, тем лучше.


### Способы регулирования работы джобы


### Известные причины поломок


### Дополнительно: тонкости и подводные камни

