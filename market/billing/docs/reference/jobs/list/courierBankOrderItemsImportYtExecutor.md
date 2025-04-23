# courierBankOrderItemsImportYtExecutor

### Код
[основной код](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/bankorder/BankOrderItemsImportYtExecutor.java?rev=95bcd93965#L23)
[Dao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/bankorder/dao/BankOrderItemImportYtDao.java?rev=476194c951#L39)

### Продукт/подсистема
Импорт детализации платежных поручений по выплатам курьерским службам и самозанятым

### Роль в работе продукта/подсистемы
Импортирует детализации платежных поручений по 1100 сервису

### Датафлоу
Запрос в YT (таблицы ARD ОЕБСа), сохранение детализации п/п в БД (market_billing.bank_order_item)

### Способы наблюдения за текущим состоянием
- Juggler-тэги:
  JOBS_PRIORITY_1, BLUE_IMPORT, DUTY_PRIORITY_HIGH

### Какая функциональность пострадает от отказа джобы
Сломается интеграция с ПРО (не будем обновлять баланс курьеров и выбивать чеки по выплатам зарплат)

### Как пользователи (или команда) заметят проблему и через какое время
курьеры не увидят выплат по сменам в приложении и изменение своего баланса

### Контакты разработчиков и менеджеров

Разработчики:
[andreybystrov](https://staff.yandex-team.ru/andreybystrov) <br/>
[va-goncharod](https://staff.yandex-team.ru/va-goncharod) <br/>
[dfirsa](https://staff.yandex-team.ru/dfirsa) <br/>
[pavel-repin](https://staff.yandex-team.ru/pavel-repin) <br/>

Менеджеры:
[yulya-solodov](https://staff.yandex-team.ru/yulya-solodov)
[tdyuldina](https://staff.yandex-team.ru/tdyuldina)


### Желательное время исправления в случае поломки
ASAP (особенно критично в дни выплат и после них 2-3 дня пока п/п отправляются в банк)

### Способы регулирования работы джобы
TBD

### Известные причины поломок
TBD

### Дополнительно: тонкости и подводные камни
TBD
