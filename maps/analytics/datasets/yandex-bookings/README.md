# Датасет бронирований
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/yandex-bookings)

- [Датасет в Datalens]()

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Хранит данные о бронированиях через вебформу.
В таблице содержатся все бронирования и фидбеки пользователей о записи.

[comment]: <> (## Для каких сервисов считается)

## Источники
Реплика базы бронирований [bookings](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/booking-int/production/data-transfer/bookings);
Реплика базы фидбеков [feedback](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/booking-int/production/data-transfer/feedback);

## Схема расчета
Бронирования джойнятся с фидбеками.

## Модель данных и описание полей
Таблица обновляется ежедневно.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
|  1|`datefield` | Дата заказа UTC |
|  2| `booking_datetime`| Дата и время записи |
|  3| `comment`| Комментарий |
|  4| `company_address`| Адрес|
|  5| `company_category_class`| Рубрика |
|  6| `company_name`| Название организации|
|  7| `created_at`| Дата и время заказа UTC|
|  8| `feedback_code` | Фидбек|
|  9| `feedback_comment`| Комментарий в фидбеке|
| 10| `feedback_created_at`| Дата и время создания фидбека UTC|
| 11| `feedback_updated_at`| Дата и время обновления фидбека UTC|
| 12| `first_order_datetime`| Дата и время первого заказа не cancelled |
| 13| `geo_id`| geo_id |
| 14| `hidden`| |
| 15| `id`| Идентификатор заказа|
| 16| `lat`|Широта |
| 17| `lon`| Долгота|
| 18| `name`| Имя пользователя |
| 19| `orders_completed`| Количество успешных заказов до этого заказа|
| 20| `os`| ios, android |
| 21| `partner_id`| Партнер записи |
| 22| `permalink`| Пермалинк организации |
| 23| `phone`| Телефон пользователя |
| 24| `puid` | Puid|
| 25| `resource_description`| Описание заказа |
| 26| `resource_id` | Id услуги|
| 27| `resource_name`| Название услуги|
| 28| `service`| Приложение где был сделан заказ |
| 29| `services_info`| |
| 30| `source`| Source |
| 31| `status`| Статус |
| 32| `tz_offset`| Разница с UTC временем|
| 33| `updated_at`| Дата и время обновления информации в заказе|


## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1).
