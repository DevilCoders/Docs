# Ежедневный расчет статистики по иконкам
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/search-icon/)

## Источники
[appmetrica-yandex-events](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-yandex-events/1d)

[navi-metrika-mobile-log](https://yt.yandex-team.ru/hahn/navigation?path=//logs/navi-metrika-mobile-log/1d)

[processed_join](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/statistics/clicks/processed_join/)

## Схема расчета
Получаю статистику по иконкам из разных источников и объединяю их (подробнее в коде)

## Модель данных и описание полей

| Название| Описание|
|----|----|
| device_id| id пользователя|
| campaign_id| id рекламной кампании|
| action| список событий (не уникальные, чтобы можно было посчитать количество)|
| service| mobile-maps, navi|
| geo_id| гео. Получаем в момент показа иконки. Берем популярный гео или выгружаем список? |
| app_platform| android, iOS|
| app_version_name| Название версии приложения |
| log_date | дата получения лога (беру из названия таблицы логов)|
| puid | id для отправки пушей|
|position| позиция иконки|
| LimitAdTracking | разрешение на трекинг рекламы|
| add_id | gaid/idfa|
|icon_name|Название иконки|

## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@
