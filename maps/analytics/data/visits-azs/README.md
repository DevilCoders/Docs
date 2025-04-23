# Данные о заездах на АЗС и проездах около них
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits_azs)

[comment]: <> (- [Датасет в Datalens]&#40;https://datalens.yandex-team.ru/datasets/gbb5tdzdmn3gc-basemap&#41;)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

* Хранит сырые данные о заездах пользователей внуть полигонов АЗС и проездах около них

* Для таблиц с заездами одна строка - факт заезда пользователя внутрь полигона АЗС

* Для таблиц с проездами - факт нахождения на дороге, ведущей к АЗС на расстоянии 250 метров от полигона

Заезд попадает в таблицу, если у пользователя было включено одно из приложений (Карты, Навигатор) во время нахождения в полигоне, неважно - свернутое или нет.
## Для каких сервисов считается

*  Навигатор
* Мобильные карты


## Источники



Логи с пользовательскими треками [travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/travel_times)

## Схема расчета

Запускаем файл [pass-by-matched-tracks/ya.make](/arc/trunk/arcadia/maps/analytics/data/pass-by-matched-tracks/ya.make). Входной параметр - таблица с полигонами объектов, для которых хотим посчитать заезды. Пример строчки с параметрами:
```angular2html
-d 20210701_ --daily -c polygon -s uuids --clids navi ymaps taxi
-i //home/zapravki/production/snippet_stations --name-field StationId
-o //home/zapravki/production/stations_stat/visits_uuids/ --mark out

```
1. Таблица с полигонами АЗС России [snippet_stations](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/snippet_stations)
2. Таблица с полигонами АЗС Турции [tr_petrol_polygons](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits-azs/turkey-polygons)

## Модель данных и описание полей
Все таблицы подневные.
1. [visits-russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits-azs/visits-russia) - заезды на АЗС России
2. [visits-turkey](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits-azs/visits-turkey) - заезды на АЗС Турции
3. [around-roads-russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits-azs/around-roads-russia) - проезды около АЗС России
4. [visits-turkey](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/visits-azs/visits-turkey) - проезды около АЗС Турции

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| clid | Приложение, для которого считаем (ru.yandex.yandexnavi, ru.yandex.mobile.navigator - Навигатор, ru.yandex.yandexmaps, ru.yandex.traffic - Карты)|
| 2|  date_time |Дата и время в UTC|
| 3|  group | Внутренний id АЗС Яндекс.Заправок (station_id из датасета заказов)|
| 4|  marked | Выехал ли пользователь с включенным Навигатором из полигона|
| 5|  time_spent | Время нахождения в полигоне (для проездов поле не имеет смысла)|
| 6|  uuid | UUID пользоватея|

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или mednikov@, lincnitnastya@.

