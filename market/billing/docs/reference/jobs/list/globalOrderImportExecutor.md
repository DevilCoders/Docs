# Импорт информаци о заказах международного Маркета

### Код

Основной код:

[класс GlobalOrderImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderImportExecutor.java)

[сервис GlobalOrderImportService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderImportService.java)

[дао GlobalCheckouterYtDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalCheckouterYtDao.java)

[дао GlobalOrderDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/global_market/GlobalOrderDao.java)

### Продукт/подсистема

Международный Маркет

### Роль в работе продукта/подсистемы

Джоба ежедневно получает информацию о заказах, выполненных за предыдущий день.

### Датафлоу

Получаем данные о заказах и товарных позициях из таблиц в YT
(`//home/market/production/global/dictionaries/billing_order` и
`//home/market/production/global/dictionaries/billing_order_item`).

По полученным данным генерируем трантаймы для обилливания, для начислений и для выплат.

Сохраняем заказы, товарные позиции и сгенерированные трантаймы в таблицы PG:

  - `market_billing.global_order`,
  - `market_billing.global_order_item`,
  - `market_billing.global_order_trantime`,
  - `market_billing.global_accrual_trantime`,
  - `market_billing.order_payout_trantime`.

### Способы наблюдения за текущим состоянием

- Juggler-проверки:
- Логи
- Изменения таблиц в БД


### Какая функциональность пострадает от отказа джобы

Не получим информацию о выполненных заказах, как следствие не сделаем выплаты и удержания, не обиллим услуги.

### Как пользователи (или команда) заметят проблему и через какое время

Загорится мониторинг о неработающей джобе (внутри `market-billing: tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:
  - [a-kolchanov](https://staff.yandex-team.ru/a-kolchanov)
  - [evmaksimenko](https://staff.yandex-team.ru/evmaksimenko)
  - [prof](https://staff.yandex-team.ru/prof)

Менеджеры:
  - ?

### Желательное время исправления в случае поломки

? Зависит от. Выплаты магазину делаем раз в неделю, поэтому:
  - в день, когда производятся выплаты, надо чинить ASAP (типа, если в 7 утра данные за вчера еще не импортированы,
    то у нас проблема);
  - в остальные дни желательно починить в ближайшие пару дней.

### Способы регулирования работы джобы

У джобы есть расписание, его можно менять в коде.

Джоба смотрит на env-переменную `market.billing.global-order-import.start-date`
(дата, с которой начинать импорт при следующем запуске) и ничего не делает,
если текущая дата >= дате из переменной. Если джоба успешно выполнилась, она обновляет значение переменной на текущую дату.

Но менять дату вручную для переимпорта данных **нельзя**. Поддержку переимпорта данных не делали.

### Известные причины поломок


### Дополнительно: тонкости и подводные камни
