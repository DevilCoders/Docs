# Ежедневный расчет статистики по иконкам
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/user-profiles-samples/30d1p)

## Источники
[cooked-metrika-mobile-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/)

[processed_join](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/statistics/clicks/processed_join/)

## Схема расчета
Получаю статистику по иконкам из разных источников и объединяю их (подробнее в коде)

## Модель данных и описание полей

|Поле|Описание|
|----|----|
| fielddate| дата получения лога|
| created_at| дата добавление статистики в таблицу|
| campaign_id| id рекламной кампании |
| platform| Сервис (navi, maps)|
| devices| Количество пользователей, которые увидели рекламу|
| icon_clicks| Клики по иконке|
| icon_shows| Показы иконок|
| shows|Показы пинов на карте после нажатия на иконку |
| clicks|Клики по пинам |
| routes|Построенные маршруты после открытия карточки |
| sites| Открытия сайтов после открытия карточки|
| calls| Нажатия на "позвонить" после открытия карточки|

## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@
