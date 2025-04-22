Обучение модели предсказания пробочных баллов
---

Процесс использует трейн-пул для обучения catboost-модели предсказания пробочных баллов в Нирване.
В процессе работы выполняет следующие действия:
- мержит таблицы из обучающего пула, подготавливаемого процессом [prepare_training_pool](/arc/trunk/arcadia/maps/analyzer/sandbox/jams_level_prediction/prepare_training_pool), сортирует результат
- запускает обучение на Нирване (создаст воркфлоу в аккаунте, токен которого был указан)
- сохраняет модель на YT и меняет линку на последнюю версию
- сохраняет модель в локальную директорию для последующей загрузки в ecstatic

Пути и параметры обучения задаются через конфиг(см. директорию [`conf`](conf)).

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/models)</br>
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/models)
