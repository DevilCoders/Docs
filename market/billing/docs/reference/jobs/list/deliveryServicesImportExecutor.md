
# deliveryServicesImportExecutor


### Код
Основной код: [класс](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/delivery/DeliveryServicesImportExecutor.java)

### Продукт/подсистема
Биллинг синего: импорты


### Роль в работе продукта/подсистемы
Импортирует данные в таблицу `shops_web.delivery_services`. Необходим для работы GOE и отчетов по услугам маркетплейса.


### Датафлоу
Оракл экспортирует данные в таблицу в YT.
Создается запрос в таблицу в YT. Оттуда забираются данные и записываются в предварительно очищенную таблицу в `Postgres`.


### Способы наблюдения за текущим состоянием
- Juggler-проверки:
- env-переменная `delivery.services.import.date` - дата последней выгрузки данных.



### Какая функциональность пострадает от отказа джобы
Формирование отчетов по услугам маркетплейса будет происходить неверно.



### Как пользователи (или команда) заметят проблему и через какое время
Только по мониторингу в juggler.



### Контакты разработчиков и менеджеров

Разработчики: [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da) <br/>


### Желательное время исправления в случае поломки
Ближайшие часы



### Способы регулирования работы джобы
- env-переменная `delivery.services.import.date` - дата последней выгрузки данных.


### Известные причины поломок
Если остановится экспорт данных из оракла в таблицу YT. Надеемся, что джобу отправки перенесут шопсы.



### Дополнительно: тонкости и подводные камни
