# dailyImportShopSkuInfoExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/stocks/DailyImportShopSkuInfoExecutor.java),
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/stocks/StockDao.java)


### Продукт/подсистема
Биллинг синего: импорты

### Роль в работе продукта/подсистемы
Джоба раз в сутки обновляет данные в PG опираясь на свежие данные в YT.


### Датафлоу
Джоба собирает данные из таблицы в каталоге `//home/market/production/mdm/dictionaries/reference_item/1d/<lastDate>`
для всех партнеров с типом `SUPPLIER` из таблицы `//home/market/production/mstat/dictionaries/partner_types/<lastDate>`,
где `lastDate` - последняя обработанная дата. И собираются точно такие же данные, но для последней даты,
существующий на текущий момент.
Выполняется запрос, ищущий разницу между двумя собранными блоками данных и результат записывается в таблицу `shops_web.shop_sku_info`.




### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  <https://juggler.yandex-team.ru/check_details/?host=market-billing&service=dailyImportShopSkuInfoExecutor&query=&last=1DAY>


### Какая функциональность пострадает от отказа джобы
Таблица перестанет быть актуальной, в связи с чем пострадают обиливания в связанных компонентах
(WithdrawBilling, ...)



### Как пользователи (или команда) заметят проблему и через какое время
Обиливания будут считаться неправильно, за счет чего могут загореться другие мониторинги.
Заметить это можно будет при закрытии месяца.



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки
Ближайшие сутки



### Способы регулирования работы джобы
env-переменные:
- **fulfillment.shop.sku.import.date** - последняя дата импорта записей
- **import.stocks.additional.logs** - нужно ли логировать дополнительные записи
- **market.mbi.import-stocks.ignored-stocks-key** - Стоки, которые нужно проигнорировать. Формат ключей должен быть: supplierId_shopSku, например, 1234_sku.
Если shopSku = "", то это означает, что нужно проигнорировать все shopSku данного поставщика (например 1234_)
- **mbi.billing.import.stocks.executor.batch.size** - размер батча. Общий со [стоками](https://docs.yandex-team.ru/market-billing/reference/jobs/list/dailyImportStocksExecutor)


### Известные причины поломок
- Слишком большой размер батча - 50000. Правится уменьшением до 5000.
- Отсутствие таблицы в Yt - правится само через несколько часов, когда появится таблица.
- Долгое время работы - проверить не отключил ли кто опцию reWriteBatchedInserts=true в [пропертях](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/properties.d/00_postgres.properties?rev=r8600887#L12)
- Долгое время работы - в прошлой версии джобы таблица забиралась целиком и tmp-yql табличка прогорала до того, как данные были сохранены целиком.


### Дополнительно: тонкости и подводные камни
Батч инсерт работает специфично ввиду косяков библиотеки. У библиотеки отсутствует возможность апдейта запросов вида
`insert ... on conflict(...) do update...`. Потому запрос написан вручную.

