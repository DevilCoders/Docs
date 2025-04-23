# tplTransactionLogCollectionExecutor

### Код

https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/config/tlog/TransactionLogJobsConfig.java?rev=0e48b9795c#L190

### Продукт/подсистема
Логистика. Выгрузка сбор услуг по ПВЗ в транзакционный лог.


### Роль в работе продукта/подсистемы
Собирает тлог из таблички `market_billing.logistic_partner_outgoing_tx` и кладет в `market_billing.tpl_transaction_log`


### Датафлоу


### Способы наблюдения за текущим состоянием
_впиши актуальные ссылки_
- Juggler-проверки:
- Логи


### Какая функциональность пострадает от отказа джобы
Не закроем месяц в логистике.

### Как пользователи (или команда) заметят проблему и через какое время

### Контакты разработчиков и менеджеров

### Желательное время исправления в случае поломки
До конца месяца

### Способы регулирования работы джобы
Env-переменные
- `market.billing.tms.tpl_tlog.collect.enabled` - включает сбор в тлог
- `market.billing.tms.tpl_tlog.export.enabled` - включает выгрузку тлога в ыть

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
