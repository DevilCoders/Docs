# Данные о заказах Яндекс.Заправок
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/zapravki-orders)

[comment]: <> (- [Датасет в Datalens]&#40;https://datalens.yandex-team.ru/datasets/7cesbudl9mto0-zapravki-orders&#41;)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Данные о заказах Заправкок. Быстрый расчет, используется, когда нужны актуальные данные о заказах, и неудобно ждать выполнения расчета "datasets/zapravki-orders"

[comment]: <> (## Для каких сервисов считается)

[comment]: <> (* Навигатор)

[comment]: <> (* Заправки)

[comment]: <> (* Мобильные карты)

[comment]: <> (* Такометр)

## Источники

Реплика базы заказов Яндекс.Заправок  [tanker_orders](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/replica/transfer-manager/mongo/tanker_orders)

Данные про АЗС [azs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/azs/2021-08-16)
## Схема расчета

Выгружаем все заказы из базы ЯндексЗаправок. Джойним с данными о АЗС
## Модель данных и описание полей
Таблица обновляется каждый час.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| order_id | Внутренний идентификатор заказа Яндекс.Заправок|
| 2|  puid |Паспортный идентификатор пользователя|
| 3|  user_id | Внутренний id пользователя Яндекс.Заправок|
| 4|  uuid |  UUID пользователя|
| 5|  device_id | DeviceID пользователя|
| 6|  uuid | UUID пользоватея|
| 7| network_id |id сети АЗС Яндекс.Заправок|
| 8|  network_name | Название сети АЗС |
| 9|  permalink |  Пермалинк АЗС из Справочника|
| 10|  bonus_card_available | Возможно ли применить карту лояльности на АЗС|
| 11|  post_pay | Постоплатная ли АЗС |
| 12| bonus_card_type | Тип карты лояльности, примененной в заказе|
| 13|  station_id |Внутренний id АЗС Яндекс.Заправок|
| 14|  station_name | Название АЗС|
| 15|  station_brand |  Бренд АЗС|
| 16|  company_id | id компании|
| 17|  application | Приложение|
| 18|  platform | Операционная система|
| 19| algoritm |Алгоритм скидки|
| 20|  bank | Банк  |
| 21|  card_id_yandex |  id банковской карты|
| 22|  card_level | Статус банковской карты|
| 23|  card_pan | Маска карты |
| 24|  create_timestamp |  Таймстемп заказа в UTC|
| 25|  event_datetime | Дата и время создания заказа (МСК)|
| 26|  feadback | Отзыв|

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или lincnitnastya@.
