## ActiveOrdersImportJob

### Продукт/подсистема

Открутки по кампании.


### Роль в работе продукта/подсистемы

Получает из БК данные по откруткам кампаний и обновляет их в базе: `campaigns.shows`, `campaigns.clicks`, `campaigns.sum_spent`, `campaigns.sum_spent_units`, `campaigns.sum_units`. Так же может менять поля: `campaigns.statusBsSynced`, `campaigns.lastShowTime`, `campaigns.stautsActive`. Это влияет на отображение баланса в интерфейсе, а так же может влиять на другую функциональность.


### Датафлоу

- Читает данные из таблицы БК [//home/yabs/stat/OrderStat](https://yt.yandex-team.ru/seneca-man/navigation?offsetMode=key&path=//home/yabs/stat/OrderStat) на сенеках. Выбирает из них самую свежую по атрибуту `last_sync_time_bs-chevent-log`.
- Джойнит с таблицами [репликатора](../../../glossary/glossary.md#b2yt) на сенеках.
- Выбирает только те кампании, по которым есть изменения в открутках, обрабатывает их, обновляет поля в mysql.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?service=jobs.ActiveOrdersImportJob.working.production&host=checks_auto.direct.yandex.ru&last=1DAY). Загорается, если джоба не завершается успешно, или если таблицы БК старее 1,5 часов.
- [Графики в Solomon](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.env=production&l.sensor=active_orders_*&graph=auto&l.shard=1&b=1d&e=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'activeorders.ActiveOrdersImportJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пострадает получение откруток - это критично. Если джоба не работает, пользователи не знают об окончании баланса, не пополняют счет, а их кампании не откручиваются.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи могут заметить прыжки в остатке не счете или статистике по откруткам при расхождении данных БК на сенеках. Пример, когда клиенты не могли заархивировать кампании из за скачков в статистике: [DIRECTSUP-35271](https://st.yandex-team.ru/DIRECTSUP-35271).


### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- Если на одном из кластеров испорчены данные, можно отключить его в конфиге [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf) в секции `dynamic-yt/order-stat-clusters`.


### Известные причины поломок

- Таблица БК очень старая (атрибут `last_sync_time_bs-chevent-log`), в этом случае обращаться в [чат статистики БК](../../../reference/chats#bs-stat). Для TS дату последнего обновления можно посмотреть [здесь](https://yt.yandex-team.ru/zeno/navigation?offsetMode=key&path=//home/direct/test/mysql-sync/testing/current/mysql-sync-states), если отстает то пишем в `Direct.Admin.Chat`.
- При учениях во Владимире БК обновляет статистику только для seneca-sas, в этом случае запросы идут только в один кластер и падают с таймаутом ([SPI-20239](https://st.yandex-team.ru/SPI-20239)).


### Дополнительно: тонкости и подводные камни

[Дока по джобе для дежурных](../../../reference/alerts/active-orders-import-job).
