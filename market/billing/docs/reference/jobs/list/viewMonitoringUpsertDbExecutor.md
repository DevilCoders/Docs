
# viewMonitoringUpsertDbExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ViewMonitoringUpsertDbExecutor.java),
[дао](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JugglerMonitoringDao.java)


### Продукт/подсистема
Биллинг синего: мониторинги представлений


### Роль в работе продукта/подсистемы
Синхронизация мониторингов представлений [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java)
с базой



### Датафлоу
Джоба раз в сутки получает список записанных мониторингов представлений из таблицы [market_billing.monitor_query_result](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/monitor_query_result.sql),
следом она апсертит их сервисы и периоды по всем элементам из энама [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java).
Если в базе оказались мониторинги, которые были удалены из энама, то джоба удаляет их.



### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  https://juggler.yandex-team.ru/check_details/?host=market-billing&service=viewMonitoringUpsertDbExecutor&query=&last=1DAY
- Ручная сверка энама [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java) и
 таблицы [market_billing.monitor_query_result](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/liquibase/market_billing/monitor_query_result.sql)



### Какая функциональность пострадает от отказа джобы
Перестанут заносится новые мониторинги и удаляться старые



### Как пользователи (или команда) заметят проблему и через какое время
Не прорастет новый моник на основе представлений, упадет моник джобы в джагглере



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Неделя



### Способы регулирования работы джобы




### Известные причины поломок
Отсутствуют



### Дополнительно: тонкости и подводные камни
