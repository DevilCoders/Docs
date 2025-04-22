Подсчет метрик для сравнения с конкуррентами
---

Считает почасовые и метрики за каждый день. Для подсчета использует логи `eta_comparison`. Для маршрутов `yandex` добавляет `route_persistent_segments` из таблицы [маршрутов](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/routes/users), все оставшиеся маршруты (конкуренты и `yandex`, которых нет в таблице) матчат к сегментам внутри процесса. После все сматченные маршруты прогоняются через `pylibs/route_stats` и обогащаются полезными метриками.

В процессе работы выполняет следующие действия:
- находит маршруты, которые и присутствуют в каждой из таблиц.
- для всех таких маршрутов геометрия матчится в `route_persistent_segments` (по способу описанному выше).
- фильтрует по покрытию и схожести маршрутов (небольшое отличие по длине).
- насчитывает `eta-metric`и для маршрутов, используя `pylibs/route_stats`, `enrich_stats` и `evaluate_metrics`.
- загружает подсчитанные метрики на YT (см. пути в [`paths.py`](lib/paths.py))

Пути до таблиц с логами берутся из тулзы, которая их загружает, см. [maps/analyzer/services/eta_comparison/lib/paths.py](/arc/trunk/arcadia/maps/analyzer/services/eta_comparison/lib/paths.py).

[Дашборд](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=8Aj)

Результаты на YT:
* [продакшн](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/eta-quality-cmp)
* [тестинг](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/testing/eta-quality-cmp)

Датасет:
* [продакшн](https://datalens.yandex-team.ru/datasets/ejjelo0x7jxk8-eta-quality-cmp)
* [тестинг](https://datalens.yandex-team.ru/datasets/49tea5j3ke5oy-eta-quality-cmp-testing)
