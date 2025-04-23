# Обработка трантаймов и создание начислений

### Код

Основной код:

класс AccrualMoneyFlowProcessingExecutor

сервис AccrualTrantimesProcessingService

[дао AccrualDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/AccrualDao.java)

дао PaymentDao

### Продукт/подсистема

Управление выплатами

### Роль в работе продукта/подсистемы

Джоба обрабатывает трантаймы и создает начисления

### Датафлоу

Получаем данные о необработанных трантаймах из таблицы
- `market_billing.accrual_trantime`

Чтобы дополнить данные для начислений, полученные данные джойним с таблицами

- `market_billing.cpa_order_transaction`,
- `market_billing.orders_transactions`,
- `market_billing.receipt_item`,
- `market_billing.cpa_order`,
- `market_billing.cpa_order_item`,
- `market_billing.service_fee_partition`

Получившееся кладем в модельку [MoneyFlowInfo](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/MoneyFlowInfo.java)

Преобразуем MoneyFlowInfo в разобранные транзакции по чеку [ParsedTransaction](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/AccrualToInsert.java)

Затем разобранные транзакции прогоняем через обработчики TransactionProcessService

И сохраняем в таблицу
- `market_billing.accrual`

### Способы наблюдения за текущим состоянием

- Juggler-проверки:
- Логи
- Изменения таблиц в БД


### Какая функциональность пострадает от отказа джобы

Не получим информацию о выполненных начислениях, как следствие не сделаем выплаты и удержания.

### Как пользователи (или команда) заметят проблему и через какое время

Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:
  - [evmaksimenko](https://staff.yandex-team.ru/evmaksimenko)

Менеджеры:
- [yaroshenko](https://staff.yandex-team.ru/yaroshenko)


### Желательное время исправления в случае поломки
Чем быстрее, тем лучше.

### Способы регулирования работы джобы

Чтобы джоба работала надо включить флаг в env
- `market.billing.AccrualTrantimesProcessingService.accrual_enabled = true`

Во избежания ООМ можно контролировать размер батча в env
- `market.billing.AccrualTrantimesProcessingService.chunkSize = 100000`

### Известные причины поломок


### Дополнительно: тонкости и подводные камни

Джоба за один запуск обрабатывает не более 20 чанков,
чтобы в предсказуемый промежуток времени сообщать в juggler об успешном выполнении работы.
