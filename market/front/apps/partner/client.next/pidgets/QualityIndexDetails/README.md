# QualityIndexDetails (Виджет в виде дровера для показа детальной информации по индексу качества)

## Скриншот

<img src="https://jing.yandex-team.ru/files/alantukh/Снимок%20экрана%202021-10-28%20в%202.37.15.png" width="300">

## Общее описание

У виджета две точки входа. Первая со страницы сводки магазина. В блоке рейтинга есть кнопка, открывающая дровер. Вторая точка входа - бизнес-страница списка индексов качества. Дровер открывается при нажатии на название любого магазина. Отмечу также, что дровер актуален и для случая, когда магазин новичов, и рейтинг еще не рассчитан.

| Права               | Поля из AppState | Модели           | Фичи кокона |
| ------------------- | ---------------- | ---------------- | ----------- |
| Доступен всем ролям | `campaignId`     | DBS/FBS/FBY/FBY+ | -           |

## Используемые бэкенды

Запрос на получение показателей индекса качества, а также данных по ограничению / отключению

[getRatingDetailedUsingGET](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/partner-rating-details-controller/getRatingDetailedUsingGET)

Запрос на получение данных для отрисовки графика с динамикой индекса качества

[getRatingDynamicUsingGET](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/partner-rating-details-controller/getRatingDynamicUsingGET)
