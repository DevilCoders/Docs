# fulfillmentRecalculateBillingExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentRecalculateBillingExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentRecalculateBillingService.java).
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentRecalculateBillingDao.java).

### Продукт/подсистема
Биллинг Синего - на текущий момент доставки

### Роль в работе продукта/подсистемы
Так как втечение месяца ВГХ некоторых ску меняются, перебилливание корректирует услуги, биллинг которых зависит от ВГХ

### Датафлоу
Джоба запускается каждые 15 минут с 01:05 ночи до 8 утра. Полезно отрабатывает один раз.
Отрабатывает при 2-х условиях:

1-Если импортировались новые ВГХ в таблицу `shops_web.shop_sku_info` джобой [DailyImportShopSkuInfoExecutor.](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/shopsku/DailyImportShopSkuInfoExecutor.java)

2-Если за этот день еще не отрабатывала (если дата `market.billing.fulfillment_recalculate_billing_service.last_date` вчерашняя)

Джоба делает запрос на расхождения ВГХ в таблице `shops_web.shop_sku_info`
и тарифа по которому обилилась услуги, (биллинг которых зависит от ВГХ) в таблице `market_billing.order_items_billed_amounts`.
Затем берет список партнеров, у которых разошлись ВГХ с тарифом, и **только по ним** перебилливает услуги, биллинг которых зависит от ВГХ
( на текущий момент доставку, отмену доставки и возвраты) с начала месяца.

### Способы наблюдения за текущим состоянием
Juggler.

И по дате в энвайрменте когда произошло последнее успешное переобиливание.
```sql
select * from shops_web.environment where name = 'market.billing.fulfillment_recalculate_billing_service.last_date';
```



### Какая функциональность пострадает от отказа джобы
На текущий момент, обилливание доставки.
СКУ у которых МДМ обновил ВГХ, доставки будет посчитана неверно за текущий месяц.


### Как пользователи (или команда) заметят проблему и через какое время
По мониторингу [Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=MON_SKU_WITH_INCORRECT_DIMENSIONS&project=market-billing&last=1DAY)

Начнут открываться тикеты от саппорта вроде [этой](https://st.yandex-team.ru/MARKETBILLING-2347)

А пользователи (магазины) будут видеть в отчетах некорректные суммы комиссий по некоторым услугам для части товаров + в итоговые акты тоже могут пролезть эти некорректные комиссии.


### Контакты разработчиков и менеджеров
Разработчики: [adjanybekov](https://staff.yandex-team.ru/adjanybekov) <br/>
[prof](https://staff.yandex-team.ru/prof) <br/>


### Желательное время исправления в случае поломки
В течение месяца влияет только на отчеты, но если не починить к закрытию месяца, партнерам будут выставлены акты с не совсем корректными суммами за некоторые услуги.


### Способы регулирования работы джобы
Джоба зависит от переменной
`market.billing.fulfillment_recalculate_billing_service.last_date`
это последняя дата когда был перебилены услуги синего маркета, которые зависят от ВГХ (на текущий момент доставки)

Эта переменная изменяется после первой успешной отработки джобы.
И благодаря изменению этой переменной джоба не отрабатывает больше одного раза в день.


### Известные причины поломок


### Дополнительно: тонкости и подводные камни
Тарифы, по которым определяем крупно/мелкогабарит, захардкожены и могут разъехаться со временем.
Поэтому надо регулярно проверять и обновлять [запрос в дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/FulfillmentRecalculateBillingDao.java)
по тарифам в [тарифнице](https://billing-admin.market.yandex.ru/tariffs?tariffIdForMetaView=2366)
