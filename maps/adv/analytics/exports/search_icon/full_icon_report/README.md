# Ежедневный расчет статистики по рекламным иконкам
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/adv/analytics/exports/search_icon/full_icon_report)

## Источники
[search-icon (mobile-maps)](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/search-icon/mobile-maps/)

[search-icon (navi)](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/search-icon/navi/)

## Схема расчета
Объединяю статистику по иконкам для МЯКа и Нави и группирую по campaign_id

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
