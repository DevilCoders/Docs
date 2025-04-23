# orderServiceReturnImportExecutor

### Код

Код джобы - https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/os/OrderServiceReturnImportExecutor.java

### Продукт/подсистема

Синий биллинг

### Роль в работе продукта/подсистемы

Джоба импортирует из Order Service возвраты и невыкупы.

Эта информация необходима для биллинга возвратов в СЦ и невыкупов.

### Датафлоу

Джоба работает через стандартный механизм - processDaysUntilYesterday.
Последовательно обрабатывает дни, начиная со значения переменной в env
[ENV_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/os/OrderServiceReturnImportExecutor.java#L17),
заканчивая вчерашним днем.

Джоба импортирует данные из таблицы в Order Service расположенной по пути:

* ['//home/market/production/mbi/order-service/out/billing/return'](https://yt.yandex-team.ru/seneca-vla/navigation?offsetMode=key&path=//home/market/production/mbi/order-service/out/billing/return)

Сохраняет данные в PG в табличку market_billing.order_service_return.

### Способы наблюдения за текущим состоянием

- Посредством логов и данных в табличке

### Какая функциональность пострадает от отказа джобы

Кратковременно - не критично (часы, несколько дней).
Долговременно и к закрытию месяца - хочется иметь информацию о возвратах/невыкупах для биллинга этих услуг.

### Как пользователи (или команда) заметят проблему и через какое время

- Посредством мониторингов

### Контакты разработчиков и менеджеров

Разработчики: [alex997](https://staff.yandex-team.ru/alex997)

### Желательное время исправления в случае поломки

Несколько дней в зависимости от того, что именно сломалось.

### Способы регулирования работы джобы

При помощи CRON и переменной в env, указывающей, начиная с какого числа нужно импортировать данные.

### Известные причины поломок

В данный момент не имеются.

### Дополнительно: тонкости и подводные камни
