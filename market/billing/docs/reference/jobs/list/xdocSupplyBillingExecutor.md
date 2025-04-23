# xdocSupplyBillingExecutor

### Код

[XdocSupplyBillingExecutor.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/xdoc/XdocSupplyBillingExecutor.java)


### Продукт/подсистема

Синий биллинг.


### Роль в работе продукта/подсистемы

Джоба обилливания поставок на транзитные склады ([wiki](https://wiki.yandex-team.ru/market/money/mbi/biznes-processy-billinga/xdoc-billing/)).


### Датафлоу

Обилливает данные по вчерашний день включительно. Текущую дату не обрабатывает.

Читает данные по поставкам:

- `market_billing.fulfillment_supply_item`
- `market_billing.fulfillment_supply`
- `shops_web.shop_sku_info`

Читает данные по тарифам:

- `market_billing.supplier_promo_tariffs` - промо-тарифы
- тарифы из Тарифницы

Пишет результат в `market_billing.xdoc_supply_billed_amount`.

### Способы наблюдения за текущим состоянием

todo


### Какая функциональность пострадает от отказа джобы

todo


### Как пользователи (или команда) заметят проблему и через какое время

todo


### Контакты разработчиков и менеджеров

Разработчики: [skiftcha](https://staff.yandex-team.ru/skiftcha), [mexicano](https://staff.yandex-team.ru/mexicano)


### Желательное время исправления в случае поломки

К концу месяца.


### Способы регулирования работы джобы

Env-переменные:
- `market.billing.xdoc_supply_billing_executor.from_date` - дата, с которой будет выполнено обилливание при запуске джобы (включительно, до текущей даты невключительно).


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

