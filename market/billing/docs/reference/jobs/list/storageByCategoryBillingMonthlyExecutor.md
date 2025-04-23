# storageByCategoryBillingMonthlyExecutor

### Код

[StorageByCategoryBillingMonthlyExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingMonthlyExecutor.java)

### Продукт/подсистема

Все тоже самое, что и [{#T}](storageByCategoryBillingExecutor.md), только работает раз в месяц и результаты уезжают в тлог.

### Роль в работе продукта/подсистемы

Ежемесячный биллинг хранения. Нужно для построения отчетности.

### Датафлоу

### Способы наблюдения за текущим состоянием

Логи по:
<br>`StorageByCategoryBillingMonthlyExecutor`
<br>`StorageByCategoryBillingService`

### Какая функциональность пострадает от отказа джобы

Биллинг хранения

### Как пользователи (или команда) заметят проблему и через какое время

Заметят проблему - загорится jobs_priority_1 в джаглере с этой джобой
Как заметят пользователи - у них будет пусто в актах по услуге хранения за предыдущий месяц

### Контакты разработчиков и менеджеров

Разработчики: [login](https://staff.yandex-team.ru/) <br/>

### Желательное время исправления в случае поломки

Сразу, как джоба упала. Потому что она работает раз в месяц и результат джобы уезжает в тлог.
Если не починить до закрытия месяца - в баланс не уедут данные по хранению оборачиваемости

### Способы регулирования работы джобы

Переменная env: `market.billing.storage_by_category_billing_monthly.start_date`

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
