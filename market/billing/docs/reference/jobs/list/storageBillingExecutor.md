# storageBillingExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageBillingExecutor.java),
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/storage/StorageBillingBilledAmountDao.java)


### Продукт/подсистема
Биллинг хранения.
### Роль в работе продукта/подсистемы
Джоба запускается каждые 30 минут, начиная с 6 утра в 00 секунд, 00 минут до 6 вечера. Биллинг хранения.


### Датафлоу

Сервис биллинга хранения. Получаем дату из env за которую нужно выполнить расчёт стоимости хранения товаров
для поставщиков.


### Способы наблюдения за текущим состоянием



### Какая функциональность пострадает от отказа джобы



### Как пользователи (или команда) заметят проблему и через какое время



### Контакты разработчиков и менеджеров



### Желательное время исправления в случае поломки



### Способы регулирования работы джобы


### Известные причины поломок


### Дополнительно: тонкости и подводные камни

