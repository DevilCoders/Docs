# Название джобы: exportStorageBillingByDepartmentExecutor

### Код

[экзекутор exportStorageBillingByDepartmentExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingByDepartmentExecutor.java)

[сервис ExportStorageBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingService.java)


### Продукт/подсистема
Биллинг хранения

### Роль в работе продукта/подсистемы
Джоба экспортирует обиленные данные по хранению оборачиваемости на ыть


### Датафлоу

Читает данные из пг из таблички **market_billing.storage_by_category_billing** [вот таким запросом](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingDao.java?rev=r9658896#L28).
Читает данные по дням.

Далее полученные данные отсылает в yt в директорию **//home/market/testing/billing/storage_turnover/by_department**. Пишет и в [хан](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/billing/storage_turnover/by_department), и в [арнольд](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/billing/storage_turnover/by_department). Для каждой даты создается отдельная табличка.
Данные отсортированы по `partner_id + departament_id`

### Способы наблюдения за текущим состоянием
Пока только общий мониторинг по джобам


### Какая функциональность пострадает от отказа джобы
Отчеты в ПИ по хранению оборачиваемости перестанут обновляться, поставщики не будут видеть актуальных данных



### Как пользователи (или команда) заметят проблему и через какое время
Будут обращаться мерчи, что данные в отчете давно не отображались
Через какое время - через сколько мерчи увидят, а увидеть они могут день в день



### Контакты разработчиков и менеджеров

Разработчики: [andreybystrov](https://staff.yandex-team.ru/andreybystrov) <br/>
Менеджеры: [nol1ght](https://staff.yandex-team.ru/nol1ght)


### Желательное время исправления в случае поломки
Как можно раньше, но не супер крит, чтобы бежать делать в первую очередь.В течение дня - нормально. На выходных скорее всего смысла нет



### Способы регулирования работы джобы
Доступных способов регулирования нет



### Известные причины поломок
На текущий момент известных причин/поломок не наблюдается



### Дополнительно: тонкости и подводные камни
1. Джоба [проверяет](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingService.java?rev=r9659398#L70), что на дату, за которую надо выгрузить данные, присутствуют обиленные подневные записи.
Джоба запускается с 3 до 6 утра каждый час. Если к **6‑му** часу данных по обиливанию не будет, то джоба так и останется гореть красной. Надо будет вручную запустить ее.
