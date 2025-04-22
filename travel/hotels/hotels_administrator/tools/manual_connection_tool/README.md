# Утилита для подключения отелей вручную через Администратор

## Сборка
`ya make -o ~/arc/arcadia`

## Использование

1. Нужно заполнить файл `hotel_data.csv` данными подключаемых отелей.
Если `agreement_end_date == null`, то в csv оставляем пустую строку.
Другие отели можно посмотреть в исторических скриптах.

Допустимые значения НДС:
* `vat_none`
* `vat_20_120`

Допустимые партнеры:
* `travelline`
* `bnovo`

Где получить accountant_email:

Зайти на https://admin.balance.yandex-team.ru/subpersons.xml?tcl_id=<balance_client_id>

### Запуск
`./manual_connection_tool --created-at '<timestamp>'`
<timestamp> - таймстемп в формате yyyy-MM-dd hh:mm:ss, например 2020-04-06 15:00:00

### Применение скриптов

Скрипт `<timestamp>/insert_hotels.sql` нужно запустить на продовой БД администратора,
* коннекшен:  `jdbc:postgresql://c-mdblb028le2km7fgdg92.rw.db.yandex.net:6432/hotels_admin?ssl=true&targetServerType=master`
* юзер: hotels_admin
* пароль тут: https://yav.yandex-team.ru/secret/sec-01e4dye05vk4qwg02ar5cc6mhy/explore/versions

### Коммитим
Для истории коммитим всё содержимое папки `<timestamp>/`
Файл `hotel_data.csv` коммитить не надо, в нем надо оставить только заголовок.

