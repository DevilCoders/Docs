# Датасет с событиями поев на карте
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/adv-filters/shows-and-clicks)

## Назначение
* В датасете выгружены все показы и клики рекламных фильтров c общими данными про запрос (гео, текст и рубрики поиска). Храним данные помесячно для более удобного использования на дашбордах.
* Для расчета кликов и показов используем уникальные значения click_id и show_id для нужного фильтра (id считаются как хеш от набора `(yandexuid, event_milli_timstamp, reqid, id, position)`)

## Для каких сервисов считается

* Веб-карты
* Тач-карты

## Источники

| Сервис | Источник | Что забираем |
|:------------- |:-------------:| -------------:|
| Веб-карты | Логи веб карт, очищенные внутренним антифродом [cooked-bebr-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-bebr-log/desktop-maps/clean&)  | Отбираем события показов и кликов на фильтр ( `'maps_www.serp_panel.results.filters.filter.carousel.item'`  с значением `is_advert` = `true`).
| Тач-карты| Логи тач карт, очищенные внутренним антифродом [cooked-bebr-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-bebr-log/touch-maps/clean&) | Отбираем события показов и кликов на фильтр ( `'maps_www.serp_panel.results.filters.filter.carousel.item'`  с значением `is_advert` = `true`).
| Общее | Таблица [бэкенда](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/geosearch-prod/snippets/input_tables/advert_chain_filter&) | Подтягиваем название фильтра и является ли рубрика рекламной `search_rubric_is_advert`.
| Общее | Данные по рубрикам [rubrics](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/geosearch-prod/geocube/1d&) | Определяем название рубрики
| Общее | Геокуб [rubrics](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/data/rubrics-classification&) | Добавляем данные про поиск - текст запроса, регион и рубрики

## Схема расчета

1. Выгружаем список reqid'ов, где были показаны или кликнуты рекламные фильтры.
2. Каждый показ и клик уникализируем как show_id или click_id (как хеш от `(yandexuid, event_milli_timstamp, reqid, id, position)` ).
3. Джойнимся с данными геокуба (serpid, текст, регион, рубрики).
4. Добавляем названия рубрик и фльтров.

## Модель данных и описание полей

**Описание полей**

|  | Поле              | Физический смысл                                                                                                                                                                                                                                           | Источник |
|:------------- |:------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| 1| click_id          | идентификатор клика на фильтр                                                                                                                                                                                                             | вычислимое |
| 2| datefield         | дата, берется  из log_date                                                                                                                                                                                                                                 | cooked-bebr-log |
| 3| filter_id         | идентификатор фильтра                                                                                                                                                                                                                             | cooked-bebr-log  |
| 4| filter_name                | название фильтра                                                                                                                                                                                                                                       | таблица бекенда |
| 5| filter_position      | позиция фильтра | cooked-bebr-log|
| 6| normal_query            | текст запроса                                                                                                                                                                                          | геокуб |
| 7| request_geo_id         | гео запроса                                                                                                                                                                                                                                  | геокуб |
| 8| search_rubric_id              | рубрика запроса                                                                                                                                                                                                                | геокуб |
| 9| search_rubric_is_advert       | является ли рубрика запроса рекламной                                                                                                                                                                                                             | таблица бекенда |
| 10| search_rubric_name | название рубрики запроса                                                                                                                                                                                                                                     | //home/maps/analytics/data/rubrics-classification |
| 11| serpid    | serpid                                                                                                                                                                                                                                         | геокуб |
| 12| show_id      | индентификатор показа фильтра                                                                                                                                                   | вычислимое |
| 14| yandexuid        | yandexuid                                                                                                                                                                                                                                              | cooked-bebr-log |


## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или hlnkzntsv@

