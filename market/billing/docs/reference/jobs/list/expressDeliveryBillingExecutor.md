# expressDeliveryBillingExecutor

### Код

[ExpressDeliveryBillingExecutor.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/express/ExpressDeliveryBillingExecutor.java)
[ExpressDeliveryBillingService.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/express/ExpressDeliveryBillingService.java)


### Продукт/подсистема

Синий биллинг.


### Роль в работе продукта/подсистемы

Джоба обилливания экспресс-доставки. Запускается каждый час начиная с 6:00.

### Датафлоу

Обилливает данные по вчерашний день включительно. Текущую дату не обрабатывает.

Читает данные по заказам:

- `market_billing.cpa_order_status_history`
- `market_billing.cpa_order`
- `shops_web.shop_sku_info`

Пишет результат в `market_billing.express_delivery_blld_amounts`.

### Способы наблюдения за текущим состоянием

- Juggler-мониторинг
- env-переменная `market.billing.express_delivery_billing_executor.start_date`


### Какая функциональность пострадает от отказа джобы

Перестанут обилливаться экспрессы.


### Как пользователи (или команда) заметят проблему и через какое время

- Juggler-мониторинг
- Придут из баланса


### Контакты разработчиков и менеджеров

Разработчики: [skiftcha](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки

К концу месяца.


### Способы регулирования работы джобы

Env-переменные:
- `market.billing.express_delivery_billing_executor.start_date` - дата, с которой будет выполнено обилливание при запуске джобы (включительно, до текущей даты невключительно).


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

