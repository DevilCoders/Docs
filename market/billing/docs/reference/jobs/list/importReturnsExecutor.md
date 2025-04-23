# importReturnsExecutor

### Код
Основной код:
[ImportReturnsExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportReturnsExecutor.kt),
[ImportReturnsService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportReturnsService.kt),
[ImportOrderReturnsService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportOrderReturnsService.java),
[ImportOrderReturnItemsService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportOrderReturnItemsService.java),
[OrderReturnDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/OrderReturnDao.kt),
[OrderReturnItemDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/OrderReturnItemDao.kt),
[OrderReturnTrantimeDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/OrderReturnTrantimeDao.kt)

### Продукт/подсистема

Импорт возвратов из YT.

### Роль в работе продукта/подсистемы

Джоба импортирует возвраты из чекаутерных выгрузок на YT.

### Датафлоу

Джоба читает данные из кластеров, указанных в проперти `yt.mbi.returns.hosts`.
По умолчанию `yt.mbi.returns.hosts=hahn.yt.yandex.net,arnold.yt.yandex.net`

Путь до таблицы с возвратами: `mbi.yt.return.path=//home/market/production/checkouter/cdc/checkouter_main/return`

Путь до таблицы с позициями возвратов: `mbi.yt.return_item.path=//home/market/production/checkouter/cdc/checkouter_main/return_item`

В одной транзакции осуществляется чтение и вставка возвратов, трантаймов для возвратов и позиций возвратов.

### Способы наблюдения за текущим состоянием
- Мониторинг Juggler

### Какая функциональность пострадает от отказа джобы

Не будут импортироваться возвраты из YT. Также не будет трантаймов по возвратам.

Это будет влиять на биллинг возвратов для услуги рассрочки.

### Как пользователи (или команда) заметят проблему и через какое время

По мониторингам

### Контакты разработчиков и менеджеров

Разработчики: [rhrrd](https://staff.yandex-team.ru/rhrrd) <br/>

### Желательное время исправления в случае поломки

сутки

### Способы регулирования работы джобы

### Известные причины поломок

### Дополнительно: тонкости и подводные камни

