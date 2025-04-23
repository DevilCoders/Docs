Оценка качества модели предсказания пробочных баллов
---

Процесс использует пул catboost-моделей предсказания пробочных баллов для расчета оффлайн и онлайн качества.

Для подсчета онлайн-качества используется флаг `-o` (`--online`).
При использовании этого флага тест-сет для расчета оффлайн-качества будет отфильтрован таким образом, что в нем останутся только те ключи (регион + час предсказания), которые есть в онлайн-логе.
При этом в результирующей табличке будут сравнимые показатели.
Процесс создает `predictions` – полные результат расчетов и `metrics` – агрегированные показатели качества.

Пути и параметры обучения задаются через конфиг(см. директорию [`conf`](conf)).

### Результаты

Predictions:
[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/quality/predictions)
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/quality/predictions)

Metrics:
[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/quality/metrics)
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/quality/metrics)
[Бэкап статбокса](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/quality/metrics/archive/raw)
[Дашборд](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=z57)
