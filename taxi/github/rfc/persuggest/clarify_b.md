# Флоу доуточнения точки Б в случае вероятного сброса с фикса

## Дизайн

https://www.figma.com/proto/erD4LPFtl7RvlumAYVEXuu/%D0%A3%D0%B2%D0%B5%D0%BB%D0%B8%D1%87%D0%B8%D0%B2%D0%B0%D0%B5%D0%BC-%D1%82%D0%BE%D1%87%D0%BD%D0%BE%D1%81%D1%82%D1%8C?page-id=483%3A21394&node-id=634%3A24806&viewport=154%2C-295%2C0.09&scaling=min-zoom&starting-point-node-id=634%3A24806

## Разработка

Будем делать новый флоу в persuggest/suggest, при включении которого меняется выдача suggest. Определять неоходимость доуточнения точки будем с помощью umlaas-geo. 

1. Как и при обычном флоу, будем ходить в карты/suggest-geo (200мс p99) за точками. В качестве основной точки будем брать первую в выдаче карт.
1. Параллельно с походом в карты, под экспериментом только для тех зон, в которых необходим флоу доуточнения, сделаем запрос в `routehistory` (150мс p99).
1. Всё это вместе (саджест карт и ответ `routehistory`) прокинем в сервис `umlaas-geo`.


Типы точек в разбиении в новой выдаче будем обозначать с помощью `additional_point_info`/`clarify_suggestion`/`point_type`. Текст про время поездки для типа точки recent будет браться из поля additional_point_info/clarify_suggestion/text, параметры для этого текста будут браться из `clarify_b_parameters.recent_text_parameters`. Для того, чтобы поддержать расширяемость на клиентах, будем присылать названия категорий в `additional_info/clarify_titles`.

## Доработки в umlaas-geo

Umlaas-geo должен уметь по некоторым данным отдавать информацию о том, нужно ли доуточнять точку или нет, ручка `umlaas-geo/v1/clarify_recommendations`, должна работать примерно 20мс p99. Апи представлено в `umlaas-geo_v1-clarify_recommendations.yaml`.

## Доработки в persuggest

Будет эксперимент, который включает новый флоу, а также содержит необходимые параметры. Схема эксперимента представлена в `clarify_b/clarify_b_parameters.yaml`.

### Новый флоу саджеста:

1. Параллельно:
	- запрос в карты /suggest-geo (200мс p99)
	- запрос в routehistory/routehistory/get (150мс p99) с `max_results=clarify_b_parameters.routehistory_max_results`

2. Дожидаемся ответа карт

3. Запрос в umlaas-geo/v1/clarify_recommendations с префиксом пользователя, саджестом карт и ответом routehistory, дожидаемся ответа.

4. Если `umlaas-geo` вернул непустой список `clarifications`, дополняем выдачу уточнениями.
