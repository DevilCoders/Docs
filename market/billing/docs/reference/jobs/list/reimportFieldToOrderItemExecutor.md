
# reimportFieldToOrderItemExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReimportFieldToOrderItemExecutor.java),
[сервис](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/checkout/reprocess/ReprocessCheckouterOrderService.java)


### Продукт/подсистема
Биллинг синего, GOE


### Роль в работе продукта/подсистемы
Реимпорт полей cat_id и fee_ue для айтмеов заказов, для которых нет этих данных


### Датафлоу
Джоба берет пачку заказов из базы у которых айтемы имеют null-ые поля. По ним ищет все айтемы в чекаутере и обновляет базу.
И так в цикле во много итераций, пока заказы не кончатся или пока не прийдет информация о флаге остановки.


### Способы наблюдения за текущим состоянием
- Juggler-проверки:
  https://juggler.yandex-team.ru/check_details/?host=market-billing&service=reimportFieldToOrderItemExecutor&query=&last=1DAY



### Какая функциональность пострадает от отказа джобы
Не будет адекватно работать обилливание фулфилмента.



### Как пользователи (или команда) заметят проблему и через какое время
Только по мониторингу в джагглер. Или когда что-то сломается, а juggler это не отобразит.



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Сутки.



### Способы регулирования работы джобы
Флаг в environment `market.billing.need_to_reimport_fields.flag` - отвечает за включение работы джобы.


### Известные причины поломок
Отсутствуют



### Дополнительно: тонкости и подводные камни
Может перегружать работу GOE.
