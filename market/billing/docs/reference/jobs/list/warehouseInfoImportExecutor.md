# warehouseInfoImportExecutor

### Код

Код джобы можно найти тут - https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/warehouse/model/WarehouseInfoImportExecutor.java

### Продукт/подсистема

Синий биллинг

### Роль в работе продукта/подсистемы

Джоба импортирует данные о складах из YT LMS.
Эта информация нужна для последующего корректного биллинга магистралей.

### Датафлоу

Читает данные из 3х таблиц LMS:

* ['home/market/production/combinator/outlets/partner'](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=home/market/production/combinator/outlets/partner)
* ['//home/market/production/combinator/outlets/logistics_point'](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/combinator/outlets/logistics_point)
* ['//home/market/production/combinator/outlets/address'](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/combinator/outlets/address)

Пример запроса - https://yql.yandex-team.ru/Operations/YehMdQVK8KlC0BDQjsfBJe1oTrEmtKkK84wt8VX_hR4=

Пишет в PG MARKET_BILLING.WAREHOUSE_INFO 4 колонки. Уникальный ключ это идентификатор склада.

**Внимание** - у нас с LMS разные понятия о складах и партнерах. Для партнер может иметь много логистических точек. Может сложиться ситуация, что когда-то уникальность не сохранится (учитывая даже текущие фильтры).

### Способы наблюдения за текущим состоянием

- Логи

### Какая функциональность пострадает от отказа джобы

Кратковременно - не критично (часы, пару дней).
Долговременно и к закрытию месяца - хочется иметь информацию о складах чтобы обиллить Магистрали. Там достаточно много денег.

### Как пользователи (или команда) заметят проблему и через какое время

Выхлоп может быть виден по обилливанию Магистралей.

### Контакты разработчиков и менеджеров

Разработчики: [teslenko](https://staff.yandex-team.ru/teslenko)

### Желательное время исправления в случае поломки

Несколько дней в зависимости от того, что именно сломалось.

### Способы регулирования работы джобы

Кроме CRON-расписания управлять ничем не получится.

### Известные причины поломок

Пока их нет. Лучше озвучивать и дополнять в будущем.

### Дополнительно: тонкости и подводные камни

Как написано выше - LMS по другому смотрит на партнеров. Для них нормально что у одного партнера множество логистических точек. Нам же нужны статические склады. Стоит обращать внимание на то, какой именно тип партнера выбирается и не расклеивается при джоинах.
