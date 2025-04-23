# jobsAggregateCreationExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JobsAggregateCreationExecutor.java),
класс аннотаций [@JugglerAggregate](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JugglerAggregate.java),


### Продукт/подсистема
Биллинг синего: мониторинги




### Роль в работе продукта/подсистемы
Создает мониторинги для всех джоб



### Датафлоу
Джоба поднимает из спрингового контекста все бины, помеченные аннотацией [@JugglerAggregate](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JugglerAggregate.java),
затем создает агрегат в джагглере со свойствами из аннотации.



### Способы наблюдения за текущим состоянием
- Juggler-проверки:https://juggler.yandex-team.ru/check_details/?host=market-billing&service=jobsAggregateCreationExecutor&project=market-billing&last=1DAY
- Логи


### Какая функциональность пострадает от отказа джобы
Перестанут формироваться агрегаты для джоб.
Заметно на примере появления новой джобы и отсутствия для нее агрегата.



### Как пользователи (или команда) заметят проблему и через какое время
Моник агрегата этой самой джобы. Отсутствие моников для новых джоб



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Неделя



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
