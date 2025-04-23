# courierExpensesTLogYtExportExecutor

### Код

https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/config/CourierPayoutsTransactionLogConfig.java?rev=1bb7e1db30#L76

### Продукт/подсистема
Биллинг логистики (курьерский)

### Роль в работе продукта/подсистемы
Выгружает данные по биллингу логистики курьерки в тлог, который читает баланс


### Датафлоу
Читает из таблички `market_billing.tpl_expenses_payouts_transaction_log`, пишет в ыть по пути `//home/market/production/billing/tlog/payouts/courier_expenses`

### Способы наблюдения за текущим состоянием
_впиши актуальные ссылки_
- Juggler-проверки:
- Логи


### Какая функциональность пострадает от отказа джобы
Не будут идти выплаты по курьерскому биллингу



### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [login](https://staff.yandex-team.ru/) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки




### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
