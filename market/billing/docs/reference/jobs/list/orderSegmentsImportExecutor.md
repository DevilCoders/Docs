# orderSegmentsImportExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/lom/OrderSegmentsImportExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/lom/OrderSegmentsImportService.java),
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/lom/OrderSegmentDao.java),
[команда](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/lom/OrderSegmentsImportCommand.java),


### Продукт/подсистема
Биллинг синего: импорты

### Роль в работе продукта/подсистемы
Импорт данных сегментов логистики из таблиц LOM-а на YT


### Датафлоу
Джоба забирает данные из таблицы на Хане `//home/cdc/prod/market/logistics_lom/waybill_segment_status_history`,
объединяя с информацией по сегментам в `//home/cdc/prod/market/logistics_lom/waybill_segment` и внешним номером заказа в
`home/cdc/prod/market/logistics_lom/orders`. Следом происходит фильтрация по статусам и запись в базу PG.



### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  <https://juggler.yandex-team.ru/check_details/?host=market-billing&service=orderSegmentsImportExecutor&query=&last=1DAY>


### Какая функциональность пострадает от отказа джобы
Некорректно будут обрабатываться невыкупы и формирование отчета по ним в услуги маркетплейса.
См. [transactionReportLogYtExportExecutor](./transactionReportLogYtExportExecutor.md)



### Как пользователи (или команда) заметят проблему и через какое время
Мониторинги, придут пользователи, что нет данных по невыкупам.



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки
До конца месяца



### Способы регулирования работы джобы
env-переменные:
- **market.billing.tms.next_segment_status_history_id** -  id из исторической таблицы статусов с которого включительно надо выгружать записи.
- **market.billing.tms.segments.import.batch.size**     - размер пачки, выгружаемой из YT за раз. По умолчанию 500_000.
- **market.billing.tms.segments.import.flag**           - флаг работы джобы. По умолчания false.
Команда OrderSegmentsImportCommand


### Известные причины поломок



### Дополнительно: тонкости и подводные камни

