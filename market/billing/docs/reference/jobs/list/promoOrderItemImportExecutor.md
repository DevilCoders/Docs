# promoOrderItemImportExecutor

### Код
Основной код:


### Продукт/подсистема
Биллинг маркетинговых услуг. БМУ


### Роль в работе продукта/подсистемы
Импортирует данные заказов по промокампании с компенсационными механиками.


### Датафлоу


### Способы наблюдения за текущим состоянием
_впиши актуальные ссылки_
- Juggler-проверки:
- Логи


### Какая функциональность пострадает от отказа джобы
Перестанут импортировать заказы -> перестанет работать биллинг -> теряем деньги


### Как пользователи (или команда) заметят проблему и через какое время


### Контакты разработчиков и менеджеров


### Желательное время исправления в случае поломки
Неделя


### Способы регулирования работы джобы
Env-переменные
`market.billing.promo_order_items_import.last_import_date` - дата с которой импортируют данные
`market.billing.promo_order_items_import.ignored_campaign_ids` - список игнорируемых campaign_id
`market.billing.promo_order_items_import.ignored_order_ids` - список игнорируемых order_id
`market.billing.promo_order_items_import.enabled` - разрешена ли работа джобы
`market.billing.promo_order_items_import.use_original_table` - писать в основную таблицу или во временную (с суффиксом _new)


### Известные причины поломок
Не доехала таблица на YT


### Дополнительно: тонкости и подводные камни
