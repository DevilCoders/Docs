# Импорт информации о партнерах международного Маркета

### Код

Основной код:

[класс GlobalPartnerContractImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalPartnerContractImportExecutor.java)

[сервис GlobalPartnerContractImportService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalPartnerContractImportService.java)

[дао GlobalCheckouterYtDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalCheckouterYtDao.java)

[дао GlobalPartnerContractDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalPartnerContractDao.java)

[дао ContractPayoutFrequencyDao](https://a.yandex-team.ru/arc_vcs/market/billing/libs-internal/core/src/main/java/ru/yandex/market/billing/core/factoring/ContractPayoutFrequencyDao.java)

### Продукт/подсистема

Международный Маркет

### Роль в работе продукта/подсистемы

Джоба ежедневно получает информацию о контрактах действующих магазинов (всех, не только новых).

### Датафлоу

Получаем данные о заказах и товарных позициях из таблиц в YT
(`//home/market/production/global/dictionaries/billing_shops`).

Полученные контракты сохраняем в таблице `market_billing.global_partner_contract`:
  - для новых магазинов просто добавляются контракты;
  - для не новых старые контракты удаляются, новые добавляются.

Для все контрактов с типом INCOME (для 610 сервиса в Балансе - перечисление средств) создаем новое или обновляем
ранее созданное расписание выплат (таблица `market_billing.client_payout_frequency`).

### Способы наблюдения за текущим состоянием

- Juggler-проверки:
- Логи
- Изменения таблиц в БД


### Какая функциональность пострадает от отказа джобы

Не получим информацию о договорах новых магазинов и изменившихся договорах старых, как следствие
не сделаем выплаты новым магазинам и сделаем некорректные выплаты старым магазинам, если у них поменялись договоры.

### Как пользователи (или команда) заметят проблему и через какое время

Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:
  - [a-kolchanov](https://staff.yandex-team.ru/a-kolchanov)
  - [prof](https://staff.yandex-team.ru/prof)

Менеджеры:
  - ?

### Желательное время исправления в случае поломки

? пока непонятно.

### Способы регулирования работы джобы

У джобы есть расписание, его можно менять в коде.

Джоба смотрит на env-переменную `market.billing.global-partner-contract-import.start-date`
(дата, с которой начинать импорт при следующем запуске) и ничего не делает,
если текущая дата >= дате из переменной. Если джоба успешно выполнилась,
она обновляет значение переменной на текущую дату.

Менять дату вручную для переимпорта данных **нельзя**, это испортит данные. Возможно, позднее за этим будем следить,
но пока просто не нужно этого делать.

### Известные причины поломок

Данные из чекаутера приезжают в каком-то неожиданном формате.

### Дополнительно: тонкости и подводные камни

Нельзя переимпортировать контракты (если за какую-то дату импорт уже случился, то заново делать импорт за эту дату не
надо, это может сломать данные).
