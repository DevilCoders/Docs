# Датасет рубричного поиска

## Назначение
Содержит информацию о совершенных рубричных поисках в гео-серивисах с детализаций по рубрике, тексту, географии поиска.

| Сервис | Ссылки |
|:------------- |:-------------:|
| Таблицы на YT | [//home/maps/analytics/datasets/rubric-search](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/rubric-search)
| Отчеты в Статистике | [Десктопные карты](https://stat.yandex-team.ru/Maps/datasets/rubric-search?scale=d&metric_key=rubric-search.sessions.count&origin=_total_&rubric_id=_total_&search_region_population_tree=%0910000%09225%09&_period_distance=30&_incl_fields=metric_value), [Тач карты](https://stat.yandex-team.ru/Maps_Mobile_All/datasets/rubric-search?scale=d&metric_key=rubric-search.sessions.count&origin=_total_&rubric_id=_total_&search_region_population_tree=%0910000%09225%09&_period_distance=30&_incl_fields=metric_value), [Мобильные карт](https://stat.yandex-team.ru/Mobile_Soft_Maps/datasets/rubric-search?scale=d&metric_key=rubric-search.sessions.count&origin=_total_&rubric_id=_total_&search_region_population_tree=%0910000%09225%09&_period_distance=30&_incl_fields=metric_value), [Навигатор](https://stat.yandex-team.ru/Mobile_Navig_Static/datasets/rubric-search?scale=d&metric_key=rubric-search.sessions.count&origin=_total_&rubric_id=_total_&search_region_population_tree=%0910000%09225%09&_period_distance=30&_incl_fields=metric_value)
| Датасет в Datalens | [датасет с данными за последний год](https://datalens.yandex-team.ru/datasets/y9bq2v4x8gmkq-main)

## Схема расчета

### Источники

| Сервис | Источник |
|:------------- |:-------------:|
| Веб-карты, Мобильные карты, Нави | Геокуб
| Общее | Классификации рубрик [rubrics](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/data/rubrics-classification&)

### Фильтр на рубричный поиск
Выполнение одного из условий
- рубричный поиск по самому точному, но менее полному классификатору  – `bus_query_type = rubric`
- рубричный поиск по позапросному DSSM классификатору с порогом `0.666459977627` (Recall >= 0.9, Precision = 0.956)
- текст поиска содержит `category_id:`. Так задаются, например, запросы про АЗС в Нави

И поиск не должен относиться к списку исключений.

Реализацию смотри в `$rubric_requests` в [common.sql](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/datasets/rubric-search/common.sql).

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики - https://t.me/joinchat/BzFEvk5zq_RILGRS03BZMw

## Отчеты и дашборды

* [Отчеты](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/reports/datasets/rubric-search)
