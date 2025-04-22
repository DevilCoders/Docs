# TplPaymentOrderDraftExecutor

### Продукт/подсистема

УВ тпл

### Роль в работе продукта/подсистемы

Джоба формирует драфты для УВ на основе тпл платежей

### Датафлоу

1. Читаем таблицу tpl_payout с null в колонке payout_group_id
2. Подбираем/создаем драфты
   в [в даошке](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/TplPaymentDraftDao.java?rev=09dfed0efd#L24)
3. Сохраняем драфт

### Способы наблюдения за текущим состоянием

- Juggler-проверки
- Логи
- Изменения таблиц в БД

### Какая функциональность пострадает от отказа джобы

Перестанут формироваться драфты на выплату для тпл

### Как пользователи (или команда) заметят проблему и через какое время

Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:

- [va-gocnharov](https://staff.yandex-team.ru/va-goncharov)
- [pavel-repin](https://staff.yandex-team.ru/pavel-repin)

Менеджеры:

- [andreybystrov](https://staff.yandex-team.ru/andreybystrov)

### Желательное время исправления в случае поломки

Чем быстрее, тем лучше.

### Способы регулирования работы джобы

Env переменная для включения/отключения джобы (true/false):

- `market.billing.CourierTransactionProcessingService.process_transactions_enabled`

Env переменная содержащяя размер батча транзакций для обработки:

- `market.billing.CourierTransactionProcessingService.chunk_size`

