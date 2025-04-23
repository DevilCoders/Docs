
# aggregateTransactionLogExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/gaap/GaapCreationExecutor.java),
[дао](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/gaap/GaapCreationYtDao.java)
[команда](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/gaap/GaapCreationCommand.java)



### Продукт/подсистема
Баланс, GAAP, Отчеты


### Роль в работе продукта/подсистемы
Создание дашборда GAAP по данным транзакционного лога.


### Датафлоу
Джоба читает данные за последние три месяца из YT таблицы тлога. Агрегирует их, совмещает с данными контрактов
партнеров из YT, преобразует и записывает в ежемесячные таблицы в YT.


### Способы наблюдения за текущим состоянием
- Мониторинг Juggler


### Какая функциональность пострадает от отказа джобы
Возникнут проблемы у баланса с отчетами по GAAP.




### Как пользователи (или команда) заметят проблему и через какое время
По мониторингам



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)


### Желательное время исправления в случае поломки
Сутки




### Способы регулирования работы джобы
Командой `GaapCreationCommand` можно перевыгрузить данные для нужного месяца


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

