# Датасет заездов на АЗС

- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/azs-visits)

[comment]: <> (- [Датасет в Datalens]&#40;https://datalens.yandex-team.ru/datasets/7cesbudl9mto0-zapravki-orders&#41;)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Хранит данные о заездах пользователей Карт и Навигатора на АЗС(только Россия).

[comment]: <> (## Для каких сервисов считается)

[comment]: <> (* Навигатор)

[comment]: <> (* Мобильные карты)


## Источники

Данные о заездах [visits-azs/visits-russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/replica/transfer-manager/mongo/tanker_orders)

Данные о подписках Яндекс.Плюс  [user-profiles-cumulative](https://yt.yandex-team.ru/hahn/navigation?path=//home/msdata/user-profiles-cumulative/v1/last)

Данные о заказах пользователей [zapravki-orders](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/zapravki-orders)

Данные про АЗС [azs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/azs/2021-08-16)
## Схема расчета
Берем свежие сырые данные о заездах, дополняем их информацией о пользователе из мобильной метрики.
Объединяем свежие данные с датасетом заездов за все предыдущие дни.
Обновляем данные о дате первого заказа в Заправках, о наличии подписки Яндекс.Плюс и данные про АЗС

## Модель данных и описание полей
Таблица обновляется ежедневно

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| application | Приложение, которое было открыто при заезде|
| 2|  puid |Паспортный идентификатор пользователя|
|3|datefield | Дата заказа (YQL тип date)|
| 4|  event_datetime | Дата и время заезда (МСК)|
| 5|  uuid |  UUID пользователя|
| 6|  device_id | DeviceID пользователя|
| 7| network_id |id сети АЗС Яндекс.Заправок|
| 8|  network_name | Название сети АЗС |
| 9|  permalink |  Пермалинк АЗС из Справочника|
| 10|  first_order_datetime | Дата и время первого заказа пользователя (по Puid)|
| 11| is_taxi_driver | Были ли у пользователя события в приложении Таксометр |
| 12| os |Операционная система пользователя|
| 13|  station_id |Внутренний id АЗС Яндекс.Заправок|
| 14|  station_name | Название АЗС|
| 15|  station_brand |  Бренд АЗС|
| 16|  station_geoid | id наименьшего региона АЗС из геобазы |
| 17|  station_stable | Подключена ли АЗС к Яндекс.Заправкам (актуальные данные) |
| 18|  user_subscription_active | Факт наличия подписки Яндекс.Плюс на текущий момент|
| 19|  time_spent | Время нахождения внутри полигона АЗС до выезда или до выключения приложения |

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или evgenstepanov@, alyasevenyuk@, mednikov@.
