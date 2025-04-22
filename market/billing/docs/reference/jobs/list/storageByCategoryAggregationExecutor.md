# storageByCategoryAggregationExecutor

### Код
[Экзекутор StorageByCategoryAggregationExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryAggregationExecutor.java)

[Сервис StorageByCategoryAggregationService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryAggregationService.java)

[Команда на предагрегацию определенных дней StorageByCategoryAggregationCommand](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/command/StorageByCategoryAggregationCommand.java)

### Продукт/подсистема

Биллинг хранения по категориям

### Роль в работе продукта/подсистемы

Сбор данных для дальнейшего обилливания

### Датафлоу
Производит подневную агрегацию данных, которые в будущем используются биллингом хранения.

Вкратце: берет данные из стоков+вгх (для расчета объема на стоках) + данные из cpa_order_item+cpa_order_status_history (для расчета проданного объема) и складываем все в **market_billing.storage_by_category_volumes**

Алгоритм смотри тут: [{#T}](../../../reference/product/storage-billing.md)

### Способы наблюдения за текущим состоянием
Общий мониторинг по джобам
Логи по:
<br>`StorageByCategoryAggregationExecutor`
<br>`StorageByCategoryAggregationService`

### Какая функциональность пострадает от отказа джобы

Биллинг хранения

### Как пользователи (или команда) заметят проблему и через какое время

Загорится общий мониторинг по джобам, который скажет, что с джобой что-то не так
Пользователи могут заметить проблему в текущий день - в отчеты в ПИ джобами exportStorageBillingBy*Executor уедут пустые данные

### Контакты разработчиков и менеджеров

Разработчики: [andreybystrov](https://staff.yandex-team.ru/andreybystrov), [makivay](https://staff.yandex-team.ru/makivay) <br/>

### Желательное время исправления в случае поломки

До конца месяца, но желательно в течение недели, т.к. результат этой джобы выгружается в yt для отчетов поставщикам.
Смотри [{#T}](exportStorageBillingBySskuExecutor.md)

### Способы регулирования работы джобы

Переменная env: `market.billing.storage_by_category_aggregation.start_date`

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
Смотри описание работы алгоритма тут: [{#T}](../../../reference/product/storage-billing.md)
