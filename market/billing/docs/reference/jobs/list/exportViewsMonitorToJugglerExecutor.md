# exportViewsMonitorToJugglerExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ExportViewsMonitorToJugglerExecutor.java)

### Продукт/подсистема
Биллинг синего: мониторинги




### Роль в работе продукта/подсистемы
Выгружает результаты работы мониторингов [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java)
из базы в juggler



### Датафлоу
Джоба собирает данные из таблицы  [market_billing.monitor_query_result](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/monitor_query_result.sql)
и выгружает их в виде сырых событий в juggler. После этого создаются примитивные агрегаты из [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java),
причем к результатам работы моника будут добавляться персональные теги из элемента энама.
Данные готовит сервис воркеров   [ViewMonitoringExecutorService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ViewMonitoringExecutorService.java?#L15)




### Способы наблюдения за текущим состоянием
- Juggler-проверки: https://juggler.yandex-team.ru/check_details/?host=market-billing&service=exportViewsMonitorToJugglerExecutor&project=market-billing&last=1DAY
- Логи


### Какая функциональность пострадает от отказа джобы
Перестанут доезжать данные мониторингов на основе представлений



### Как пользователи (или команда) заметят проблему и через какое время
Как моник загорится или полетят критами NO_DATA



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки
Ближайшие часы



### Способы регулирования работы джобы




### Известные причины поломок
Недоступен сервер juggler. Обычно правится само.



### Дополнительно: тонкости и подводные камни
