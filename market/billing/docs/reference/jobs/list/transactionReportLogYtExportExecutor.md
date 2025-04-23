
# transactionReportLogYtExportExecutor

### Код
[класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/marketplace/TransactionReportLogYtExportExecutor.java),
[сервис](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/marketplace/TransactionReportLogYtService.java),
[команда](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/marketplace/model/TransactionReportLogYtExportCommand.java)

### Продукт/подсистема
Отчеты синего: отчет по услугам маркетплейса(Стоимость услуг)

### Роль в работе продукта/подсистемы
Выгрузка данных расширенного тлога в YT для формирования отчетов в монолите.

### Датафлоу
Пачками читает транзакционный лог в PG, обрабатывает строки по типам продукта, формирует из них дополнительное поле
и, обернутыми в транзакцию, отправляет, в YT:
[Таблицы](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mbi/billing/tlog-report/revenues)


### Способы наблюдения за текущим состоянием
- Логи
- [Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=transactionReportLogYtExportExecutor&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы
Не будут формироваться отчеты

### Как пользователи (или команда) заметят проблему и через какое время
Придут партнеры или джагглер.


### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da/)

### Желательное время исправления в случае поломки
По возможности

### Способы регулирования работы джобы
**Следующие env-переменные**:
* `market.billing.tms.tlog-report.export` - флаг работы джобы. Можно отключить таким образом экспорт расширенного тлога
* `market.billing.tms.tlog-report.export.batch-size` - размер одновременно обрабатываемой пачки транзакций. По умолчанию 50_000
* `market.billing.tms.tlog-report.export.alter-path` - использовать ли альтернативную папку для выгрузки(вместо revenues - revenues-copy)
* `market.billing.tms.tlog-report.export.transactions_info` - json, хранящий информации об id последней выгруженной записи, id будущей записи и ее eventDate
Записывается в следующем виде: `{"lastTransactionId":#,"futureTransactionId":#,"tableName":"yyyy-mm-dd"}`.
* `market.billing.tms.tlog-report.export.command.transactions_info` - json, аналогичный енву выше, но для работы команды.
**Команда**:(использовать только для выгрузки в другую папку)
Пример команды на экспорт транзакций из полуинтервала [10000;20000):
```
export-tlog-report --from=10000 --to=20000
--use_alter_path - писать в другую папку (вместо revenues - revenues-copy)
--continue - продолжить работу прерванной команды с того же места и до --to
```


### Известные причины поломок
Добавляют новые услуги, не создав соответствующих маппер, или меняют ключевое поле в тлоге, которое не удается распарсить.


### Дополнительно: тонкости и подводные камни
Если **lastTransactionId** и **futureTransactionId** в `market.billing.tms.tlog-report.export.transactions_info` совпадают, значит это
последняя выгруженная транзакция. Иначе надо сравнивать **futureTransactionId** в максимальном айди из **tableName**, если она есть.
Если id не равны или таблицы нет, значит номер последней транзакции это **lastTransactionId**. Иначе **futureTransactionId**.

