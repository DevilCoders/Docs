# CourierTransactionProcessingExecutor

### Код

- [Джоба](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/TplCourierTransactionToAccrualExecutor.java)
- [Сервис](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/CourierTransactionProcessingService.java)
- [Дао MoneyFlowTransactionDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/tpl/courier/MoneyFlowTransactionDao.java)
- [Дао TplAccrualDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/TplAccrualDao.java)

### Продукт/подсистема

УВ биллинга логистики

### Роль в работе продукта/подсистемы

Джоба обрабатывает курьерские транзакции, получаемые из tpl-биллинга, и на основе них создает начисления.

### Датафлоу

Читаем необработанные записи из:
- `market_billing.tpl_transaction`

Полученные данные кладем в модельку [MoneyFlowTransaction](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/tpl/courier/MoneyFlowTransaction.java)

Обрабатываем TplTransaction и получаем модельку [TplAccrual](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/TplAccrual.java)

Сохраняем TplAccrual в табличку:
- `market_billing.tpl_accrual`

Проставляем признак обработанности (`processed = true`) в табличке:
- `market_billing.tpl_transaction`

### Способы наблюдения за текущим состоянием

- Juggler-проверки
- Логи
- Изменения таблиц в БД


### Какая функциональность пострадает от отказа джобы

Перестанут формироваться начисления для курьерских служб, и как следствие не будут производится выплаты этим службам.

### Как пользователи (или команда) заметят проблему и через какое время

Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:
- [dfirsa](https://staff.yandex-team.ru/dfirsa)
- [pavel-repin](https://staff.yandex-team.ru/pavel-repin)
- [va-gocnharov](https://staff.yandex-team.ru/va-goncharov)

Менеджеры:
- [yaroshenko](https://staff.yandex-team.ru/yaroshenko)


### Желательное время исправления в случае поломки

Чем быстрее, тем лучше.

### Способы регулирования работы джобы

Env переменная для включения/отключения джобы (true/false):
- `market.billing.CourierTransactionProcessingService.process_transactions_enabled`

Env переменная содержащяя размер батча транзакций для обработки:
- `market.billing.CourierTransactionProcessingService.chunk_size`

### Известные причины поломок




### Дополнительно: тонкости и подводные камни

