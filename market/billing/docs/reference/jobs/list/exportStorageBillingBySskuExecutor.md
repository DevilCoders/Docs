# Название джобы: exportStorageBillingBySskuExecutor

### Код

[экзекутор exportStorageBillingBySskuExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingBySskuExecutor.java)

[сервис ExportStorageBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingService.java)


### Продукт/подсистема
Синий биллинг

### Роль в работе продукта/подсистемы
Джоба экспортируем обиленные данные по хранению оборачиваемости в разрезе shop sku на ыть


### Датафлоу

Читает данные из пг из таблички **storage_by_category_volumes** [вот таким запросом](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingDao.java?rev=r9658896#L58).
Пользователю нужны агрегированные данные за отчетный период (то есть с 1ого числа месяца по текущую дату). Поэтому запрос делает следующее:
1. Собирает агрегированные данные (среднесуточный объем стока по sku и среднесуточный объем продаж по shop sku) за дни [1ое число месяца, требуемый день] (обе даты включительно)
2. Считает количество стока на последний день в отчетном периоде (т.е. на требуемый день). Сток = `available + expired + defect`
3. Полученные данные отдает наружу
Далее полученные данные отсылает в yt в директорию **//home/market/testing/billing/storage_turnover/by_ssku**. Пишет и в [хан](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/billing/storage_turnover/by_ssku), и в [арнольд](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/billing/storage_turnover/by_ssku). Для каждой даты создается отдельная табличка.
Данные отсортированы по [partner_id + departament_id + shop_sku](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingService.java?rev=r9659398#L40)


### Способы наблюдения за текущим состоянием
Пока только общий мониторинг по джобам


### Какая функциональность пострадает от отказа джобы
Отчеты в ПИ по хранению оборачиваемости по shop sku перестанут обновляться, поставщики не будут видеть актуальных данных



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
1. Джоба [проверяет](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/export/ExportStorageBillingService.java?rev=r9659398#L93), что на дату, за которую надо выгрузить данные, присутствуют агрегированные записи по обиливанию хранения
   Джоба запускается с 3 до 6 утра каждый час в 10 минут. Если к 6‑му часу данных по агрегированию не будет, то джоба так и останется гореть красной. Надо будет вручную запустить ее.

