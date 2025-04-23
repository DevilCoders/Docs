Подготовка датасета с историей пробочных баллов
---

Процесс использует таблицы с почасовой историей пробочных баллов на yt

В процессе работы выполняет следующие действия:
- мержит таблицы с почасовой историей пробочных баллов, подготавливаемые процессом [prepare_history](/arc/trunk/arcadia/maps/analyzer/sandbox/jams_level_prediction/prepare_history)
- читает результат мержа и подает на вход локально запускаемому бинарнику, который создает бинарный файл с историей (mms)
- сохраняет файл на YT
- сохраняет файл в локальную директорию для последующей загрузки в ecstatic

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/history_storage)
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/history_storage)

датасет в ecstatic – yandex-maps-jams-level-history-storage
