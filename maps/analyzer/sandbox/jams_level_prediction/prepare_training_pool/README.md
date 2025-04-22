Подготовка трейн-пула для обучения модели предсказания пробочных баллов
---

Процесс использует таблицы с полной и почасовой историей пробочных баллов, а также датасет с историей баллов

В процессе работы выполняет следующие действия:
- для каждого дня находит полную (элементы обучающей выборки) и почасовые (значения используются в качестве таргета), за даты в зависимости от значений лага предсказания, истории баллов, подготавливаемые процессом [prepare_history](/arc/trunk/arcadia/maps/analyzer/sandbox/jams_level_prediction/prepare_history), а также датасет с историей, подготавливаемый процессом [prepare_history_storage](/arc/trunk/arcadia/maps/analyzer/sandbox/levl_prediction/prepare_history_storage)
- на основе вышеописанных данных запускает mapreduce-операцию расчета фичей, использующую библиотеку [jams_level_prediction](/arc/trunk/arcadia/maps/analyzer/libs/jams_level_prediction)
- сохраняет таблицу с фичами в TSV-формате на yt

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/pool)
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/pool)
