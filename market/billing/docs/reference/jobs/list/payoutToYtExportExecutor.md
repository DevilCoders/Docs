# payoutToYtExportExecutor

### Код

Основной код:

[класс PayoutToYtExportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PayoutToYtExportExecutor.java)

[сервис PayoutDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/services/PayoutYtService.java)

[дао PayoutDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/payment/dao/PayoutDao.java)

### Продукт/подсистема

Управление выплатами

### Роль в работе продукта/подсистемы

Выгружает таблицу `market_billing.payout` в YT кластер hahnYt `//home/market/production/billing/dictionaries/payment_control/payout`


### Датафлоу

Джоба запускается каждый час начиная с в 8 часов утра.
Читает все обработанные данные (_payout_group_id not null_) из таблицы

- `market_billing.payout`

начиная с даты в env (_market.billing.payout_to_yt_export_executor.start_date_) до вчерашнего дня

Пишет в кластер hahnYt `//home/market/production/billing/dictionaries/payment_control/payout`

При наличие необработанных данных за день, джоба падает с ошибкой `{N} unprocessed payouts found exception on {date}`

### Способы наблюдения за текущим состоянием

- Juggler-проверки:
- Логи
- Изменения таблиц в БД


### Какая функциональность пострадает от отказа джобы
Отчеты и сверки

### Как пользователи (или команда) заметят проблему и через какое время
Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

Дежурный заметит что упадут сверки, в течение нескольких часов

Поставщики заметят что нет данных в отчетах

### Контакты разработчиков и менеджеров

Разработчики:
- [adjanybekov](https://staff.yandex-team.ru/adjanybekov)
- [a-kolchanov](https://staff.yandex-team.ru/a-kolchanov)

### Желательное время исправления в случае поломки
24 часа



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

