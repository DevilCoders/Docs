
# viewMonitorTimeoutSetterExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ViewMonitorTimeoutSetterExecutor.java),
[дао](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JugglerMonitoringDao.java)


### Продукт/подсистема
Биллинг синего: мониторинги представлений


### Роль в работе продукта/подсистемы
Проставляет таймауты зависшим запросам представлений.



### Датафлоу
Каждые полчаса джоба обновляет данные в таблице [market_billing.monitor_query_result](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/monitor_query_result.sql),
для тех записей, время выполнения которых превышает их период в `N` раз. См. подробнее [{#T}](#job-regulation)



### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  https://juggler.yandex-team.ru/check_details/?host=market-billing&service=viewMonitorTimeoutSetterExecutor&query=&last=1DAY



### Какая функциональность пострадает от отказа джобы
Все мониторинги могут повиснуть в статусе processing и juggler перестанет обновляться.



### Как пользователи (или команда) заметят проблему и через какое время
Juggler-мониторинг джобы



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
День



### Способы регулирования работы джобы { #job-regulation }
Env-переменная
- `market.billing.tms.views_monitor.timeout.multiplier` - значение множителя периодов, после превышения перемножения которых ставится статус TIMEOUT.
По умолчанию принимает значение статической переменной [DEFAULT_TIMEOUT_PERIOD_MULTIPLIER](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ViewMonitorTimeoutSetterExecutor.java#L15) равное 3.




### Известные причины поломок
Отсутствуют



### Дополнительно: тонкости и подводные камни
Несмотря на проставление таймаутов, работа тредов не прерывается, что может вызвать дополнительные проблемы.
