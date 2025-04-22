# reprocessCheckouterOrderExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReprocessCheckouterOrderExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReprocessCheckouterOrderService.java),


### Продукт/подсистема
Биллинг синего, GOE

### Роль в работе продукта/подсистемы
Организует непрерывную и корректную работу сервисов обилливания и выгрузки расширенного тлога, дополняя ошибки GOE.

### Датафлоу
Джоба запускается каждый час. Проверяет включен ли флаг и если да, то просматривает таблицу shops_web.environment
на предмет заказов, которые необходимо перезагрузить из чекаутера.


### Способы наблюдения за текущим состоянием
Juggler
monitor-oracle-to-postgres - пока включен оракл


### Какая функциональность пострадает от отказа джобы
Ошибки в расширенном тлоге и таблицах с обилливаниями


### Как пользователи (или команда) заметят проблему и через какое время
Моники, нестыковки в отчетах.



### Контакты разработчиков и менеджеров
Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки



### Способы регулирования работы джобы


### Известные причины поломок


### Дополнительно: тонкости и подводные камни

