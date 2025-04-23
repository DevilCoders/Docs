# transactionsSolomonExportExecutor
### Код

[класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/solomon/TransactionsSolomonExportExecutor.java)

### Продукт/подсистема
Единый транзакционный лог:экспорты в соломон

### Роль в работе продукта/подсистемы
Отдаёт в solomon информацию по невыгруженным в единый тлог транзакциям

### Датафлоу
Читает таблицу в PG: market_billing.not_exported_tlog_collection <br/>
Отдаёт метрики в [сенсор соломона](https://solomon.yandex-team.ru/?project=market-billing&cluster=agent-metrics&service=market-billing-tms&l.sensor=not_exported_to_tlog_transactions.count.*&graph=auto) (через pull)


### Способы наблюдения за текущим состоянием
- обновление данных в сенсоре соломона
- Логи
- [Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=transactionsSolomonExportExecutor&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы
не будет информации о количестве неэкспортированных тлогов в соломоне

### Как пользователи (или команда) заметят проблему и через какое время
Отсутствие новых данных в соломоне, мониторинг в джагглере


### Контакты разработчиков и менеджеров

Разработчики: [phillippko](https://staff.yandex-team.ru/phillippko/)

### Желательное время исправления в случае поломки
По возможности

### Способы регулирования работы джобы
Отключение джобы


### Известные причины поломок
Отсутствуют


### Дополнительно: тонкости и подводные камни

