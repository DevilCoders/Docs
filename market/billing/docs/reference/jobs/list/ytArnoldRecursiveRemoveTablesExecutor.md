# ytArnoldRecursiveRemoveTablesExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/clearing/yt/YtRecursiveRemoveTablesExecutor.java),
[cервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/clearing/yt/YtRecursiveRemoveService.java)


### Продукт/подсистема
YT/лимиты чанков и нод.

### Роль в работе продукта/подсистемы
Удаление таблиц, старше 42 дней в тестинге Арнольда YT.
См. также [ytHahnRecursiveRemoveTablesExecutor](./ytHahnRecursiveRemoveTablesExecutor.md)


### Датафлоу
Рекурсивно, начиная с `//home/market/testing/billing`, создается список всех таблиц, а затем удаляются все старше 42.
Если таблицы должны удалиться все - остается только одна, последняя измененная.


### Способы наблюдения за текущим состоянием
Juggler-мониторинг


### Какая функциональность пострадает от отказа джобы
Ноды и чанки будут медленно копиться.


### Как пользователи (или команда) заметят проблему и через какое время
Juggler-мониторинг


### Контакты разработчиков и менеджеров
Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Неделя


### Способы регулирования работы джобы


### Известные причины поломок
Битые ссылки по некоторым путям. Джобе не удается получить по ним данные.

### Дополнительно: тонкости и подводные камни

