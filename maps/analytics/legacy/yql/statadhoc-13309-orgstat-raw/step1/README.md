# Step1: `processed_join`

## Назначение
Расчет таблиц, которые хранят факты открытий карточек с действиями внутри карточки и другой полезной информацией. Одна строка - это уникальный кортеж `(userid, reqid, permalink)`.

На основе этих данных построен датасет для быстрого просмотра статистики организаций за [последние 30 дней](https://wiki.yandex-team.ru/maps/analytics/tools/#statistikaorganizacijj) и начиная [с января 2019](https://wiki.yandex-team.ru/maps/analytics/tools/#statistikaorganizacijjsjanvarja2019).

| Сервис | Ссылки |
|:------------- |:-------------:|
| Таблицы на YT | [//home/geoadv/statistics/clicks/processed_join](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/statistics/clicks/processed_join)
| Реакция | TBA
| Артефакты | TBA

## Схема расчета

1. По клиентскому логу составляем таблицу открытий карточек
1. По клиентскому логу группируем клики на карточке
1. Читаем `map-reqans-log`, разворачиваем список ответов
1. Составляем дополнительные таблицы для обогащения открытий специфичные для сервиса. Например, классификация фрода для веб-карт.
1. К п.1 делаем left join остальных таблиц по кортежу. В итоге имеем все открытия карточек на сервисе с дополненной информацией
1. Переводим сырые клики на карточке в действия (`actions`) на основе  [clicks_description.json](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/geo/maps/common/clicks_description.json)
1. Классифицируем открытия по сценариям

### Пересчет классификации сценариев и кликов
Чтобы пересчитать классификацию сценариев и/или клики, то следуюет
1. [Закомментировать](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/jam/jobs/regular_jobs/geo-analytics/statadhoc-13309/step1/export_clicks_step_1.yql?rev=7360130#L858) запись таблиц тхе сервисов для которых не нужен пересчет
2. Запустить команду пересчета
```
ikolodkin@jupyter-cloud-ikolodkin:~/arc/arcadia/statbox/jam/jobs/regular_jobs/geo-analytics/statadhoc-13309/step1$ make reclassify_history START_DATE=2020-06-12 FINISH_DATE=2020-08-19
```
В результате для каждой даты последовательно будет запущен YQL, который читает `processed_join`, обновляет поля классфикации сценарием и кликов и заменяет старую таблицу.

## К кому можно обращаться с вопросами

Вопросы задавать можно ikolodkin@, ayunts@

## Отчеты и дашборды

* [Отчеты](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/reports/datasets/rubric-search)
