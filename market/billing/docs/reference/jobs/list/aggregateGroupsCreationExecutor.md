# aggregateGroupsCreationExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/AggregateGroupsCreationExecutor.java)

### Продукт/подсистема
Биллинг синего: мониторинги




### Роль в работе продукта/подсистемы
Создает групповые мониторинги для джоб по энаму [MonitorJobsGroups](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorJobsGroups.java)
и для мониторингов на основе представлений из энама [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java)




### Датафлоу
Джоба проходится по обоим энамам по очереди, для каждой новой группы проходится по всем джобам/представлениям и собирает данные
с тем же групповым именем, после чего отправляет в juggler команда на создание агрегата.



### Способы наблюдения за текущим состоянием
- Juggler-проверки: https://juggler.yandex-team.ru/check_details/?host=market-billing&service=aggregateGroupsCreationExecutor&project=market-billing&last=1DAY
- Логи


### Какая функциональность пострадает от отказа джобы
Перестанут создаваться групповые агрегаты. Не критично, но пострадает удобство.



### Как пользователи (или команда) заметят проблему и через какое время
По juggler-мониторингу, если джоба упадет



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/) <br/>


### Желательное время исправления в случае поломки
Неделя



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
Если нет имени группового агрегата для какого-то представления из [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java)
- он не создается
