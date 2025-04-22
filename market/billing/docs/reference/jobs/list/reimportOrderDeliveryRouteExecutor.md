
# reimportFieldToOrderItemExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReimportOrderDeliveryRouteExecutor.java),
[сервис](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReprocessCheckouterOrderService.java)


### Продукт/подсистема
Биллинг синего, GOE


### Роль в работе продукта/подсистемы
Необходимо для реимопрта регионов для магистралей и отчетов по услугам маркетплейса.


### Датафлоу
Джоба берет пачку заказов из базы у которых поле region_to пусто. Эти заказы ищутся в чекаутере и следом обновляется поле в базе.
И так в цикле во много итераций, пока заказы не кончатся или пока не прийдет информация о флаге остановки.


### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  https://juggler.yandex-team.ru/check_details/?host=market-billing&service=reimportOrderDeliveryRouteExecutor&query=&last=1DAY



### Какая функциональность пострадает от отказа джобы
Невозможно будет корректно посчитать отчеты и обиллить магистрали.



### Как пользователи (или команда) заметят проблему и через какое время
Только по мониторингу в джагглер. Или когда что-то сломается, а juggler это не отобразит.



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Сутки.



### Способы регулирования работы джобы
Флаг в environment `market.billing.need_to_reimport_order_regions.flag` - отвечает за включение работы джобы.
Переменная в environment `market.billing.reimport_order_regions.dateg` - с какой даты мы ищем подобные заказы для реимпорта.


### Известные причины поломок
Отсутствуют



### Дополнительно: тонкости и подводные камни
Может перегружать работу GOE.
