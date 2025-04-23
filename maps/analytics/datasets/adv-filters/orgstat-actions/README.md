# Датасет с событиями поев на карте
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/adv-filters/shows-and-clicks)

## Назначение
* В датасете выгружены все действия в карточках организация после клика на рекламный фильтр. Храним данные помесячно для более удобного использования на дашбордах.
* Для расчета открытия карточек используем уникальные значения open_card_id - считается как хеш `(yandexuid, reqid, permalink)`)

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
| Общее | [processed_join](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/geoadv/statistics/clicks/processed_join/s&) | Добавляем данные про действия в карточках
## Схема расчета

1. Выгружаем список reqid'ов, где кликали на рекламные фильтры. По reqid'ам определяем список serpid'ов, где кликнули на фильтры.
2. Достаем из proccesed_join'a все действия с карточками после клика на фильтр; генерируем open_card_id для уникализации на дашборде.
3. Джойнимся с данными геокуба (serpid, текст, регион, рубрики).
4. Добавляем данные про названия фильтров и организаций.

## Модель данных и описание полей

**Описание полей**

|  | Поле              | Физический смысл                                                                                                                                                                                                                                           | Источник |
|:------------- |:------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| 1| any_site          | был ли открыт сайт в карточке орги                                                                                                                                                                                                             | processed-join |
| 2| build_route         | был ли построен маршрут из карточки оргиорги                                                                                                                                                                                                                                 | processed-join |
| 3| company_name         | название компании                                                                                                                                                                                                                            | common/company_pretty_format  |
| 4| datefield                | дата                                                                                                                                                                                                                                        | cooked-bebr-log |
| 5| filter_id         | идентификатор фильтра                                                                                                                                                                                                                             | cooked-bebr-log  |
| 6| filter_name                | название фильтра   
| 7| filter_position      | позиция фильтра | cooked-bebr-log|
| 8| geoproduct_cta            | был ли cta в карточке орги                                                                                                                                                                                          | processed-join |
| 9| geoproduct_offer_open         | был ли открыт оффер в карточке орги                                                                                                                                                                                                                              | processed-join |
| 10| permalink              | пермалинк орги                                                                                                                                                                                                                | геокуб |
|11| search_rubric_id              | рубрика запроса                                                                                                                                                                                                                | геокуб |
| 12| search_rubric_is_advert       | является ли рубрика запроса рекламной                                                                                                                                                                                                             | processed-join |
| 13| search_rubric_name | название рубрики запроса                                                                                                                                                                                                                                     | //home/maps/analytics/data/rubrics-classification |
| 14| serpid    | serpid                                                                                                                                                                                                                                         | геокуб |
| 15| phone      | совершали ли телефонный звонок из карточки орги                                                                                                                                                   | processed-join |
| 16| yandexuid        | yandexuid                                                                                                                                                                                                                                              | cooked-bebr-log |


## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или hlnkzntsv@

