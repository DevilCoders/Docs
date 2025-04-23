# sortingOrderBillingExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/sorting/SortingOrderBillingExecutor.java),
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/sorting/SortingBillingDao.java)


### Продукт/подсистема
Обилливание сортировки заказов.

### Роль в работе продукта/подсистемы
Джоба запускается каждый час, начиная с 6:15. Биллинг сортировки заказов на синем маркете.


### Датафлоу

Сервис обилливания услуг сортировки заказов на синем маркете.  Обилливание по заказам смотрит на 2 источника данных - заказы dropship'а из
таблицы <code>market_billing.order_trantimes</code> и <code>market_billing.logistic_orders</code>.


### Способы наблюдения за текущим состоянием



### Какая функциональность пострадает от отказа джобы



### Как пользователи (или команда) заметят проблему и через какое время



### Контакты разработчиков и менеджеров



### Желательное время исправления в случае поломки



### Способы регулирования работы джобы


### Известные причины поломок


### Дополнительно: тонкости и подводные камни

