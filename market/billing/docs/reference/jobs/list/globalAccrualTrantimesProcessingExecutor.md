# Обработка глобальных трантаймов и создание начислений

### Код

Основной код:

[класс GlobalAccrualTrantimesProcessingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/GlobalAccrualTrantimesProcessingExecutor.java)

[сервис GlobalAccrualTrantimesProcessingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/GlobalAccrualTrantimesProcessingService.java)

[дао AccrualDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/AccrualDao.java)

[дао GlobalOrderDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderDao.java)

### Продукт/подсистема

Международный Маркет

### Роль в работе продукта/подсистемы

Джоба ежедневно обрабатывает глобальные трантаймы и создает начисления

### Датафлоу

Получаем данные о необработанных глобальных трантаймах из таблицы
- `market_billing.global_accrual_trantime`

Чтобы дополнить данные для начислений, полученные данные джойним с таблицами

- `market_billing.global_order`,
- `market_billing.global_order_item`

Получившееся кладем в модельку [MoneyFlowInfo](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/MoneyFlowInfo.java)

Обрабатываем MoneyFlowInfo и готовим модельку для создания начислений [AccrualToInsert](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/model/AccrualToInsert.java)

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
  - [a-kolchanov](https://staff.yandex-team.ru/a-kolchanov)
  - [evmaksimenko](https://staff.yandex-team.ru/evmaksimenko)
  - [prof](https://staff.yandex-team.ru/prof)
  - [adjanybekov](https://staff.yandex-team.ru/adjanybekov)

Менеджеры:
- [yaroshenko](https://staff.yandex-team.ru/yaroshenko)


### Желательное время исправления в случае поломки
Чем быстрее, тем лучше.

### Способы регулирования работы джобы

Чтобы джоба работала надо включить флаг в env
- `market.billing.GlobalAccrualTrantimesProcessingService.global_accrual_enabled = true`

Во избежания ООМ можно контролировать размер батча в env
- `market.billing.GlobalAccrualTrantimesProcessingService.chunkSize = 100000`

### Известные причины поломок


### Дополнительно: тонкости и подводные камни
