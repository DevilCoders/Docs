# Yet another top directions calculation

Ещё одна реализация подсчёта популярных направлений.
Расчёт основан на логах `//home/avia/logs/avia-users-search-log/`.
Аналогичный расчёт производится:
1. для таблицы //home/avia/popular_directions в
RUN_YQL sandbox задаче
2. для таблицы avia_data/topdirection в админке.

Ещё одна релизация нужна потому что №1 содержит только 200 направлений,
а №2 лежит только в базе данных.

Путь для сохранения по умолчанию
* для тестинга
`//home/avia/testing/data/ad-feed/top-directions`
* для прода
`//home/avia/data/ad-feed/top-directions`


