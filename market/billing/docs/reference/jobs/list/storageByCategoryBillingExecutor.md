# storageByCategoryBillingExecutor

### Код

[StorageByCategoryBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingExecutor.java)
[Команда для расчета конкретного дня StorageByCategoryBillingCommand](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/command/StorageByCategoryBillingCommand.java)

### Продукт/подсистема

Биллинг хранения по категориям

### Роль в работе продукта/подсистемы

Ежедневный биллинг хранения. Нужно для построения отчетности.

### Датафлоу
Собирает данные из предагрегированных данных (которые поставляет [#{T}](storageByCategoryAggregationExecutor.md)) и складывает данные в табличку **market_billing.storage_by_category_billing**
Дальше эти данные уезжают в отчеты в ПИ в рамках [#{T}](exportStorageBillingByDepartmentExecutor.md)

### Способы наблюдения за текущим состоянием
Общий мониторинг по джобам
Логи по:
<br>`StorageByCategoryBillingExecutor`
<br>`StorageByCategoryBillingService`

### Какая функциональность пострадает от отказа джобы

Биллинг хранения (и отчеты (в пи и оумп), т.к. они связаны с биллингом хранения)

### Как пользователи (или команда) заметят проблему и через какое время

Загорится общий мониторинг по джобам, который скажет, что с джобой что-то не так
Пользователи могут заметить проблему в текущий день - в отчеты в ПИ джобами exportStorageBillingBy*Executor уедут пустые данные

### Контакты разработчиков и менеджеров

Разработчики: [andreybystrov](https://staff.yandex-team.ru/andreybystrov), [makivay](https://staff.yandex-team.ru/makivay) <br/>

### Желательное время исправления в случае поломки

До конца месяца, но желательно в течении недели, т.к. результаты этой джобы выгружаются в yt для отчетов поставщикам.
см [#{T}](exportStorageBillingByDepartmentExecutor.md)у

### Способы регулирования работы джобы

Переменная env: `market.billing.storage_by_category_billing.start_date`

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
описание алгоритма смотрит тут [{#T}](../../../reference/product/storage-billing.md#---1--2022--new-billing-)
