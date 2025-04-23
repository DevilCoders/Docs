# Объекты для сбора данных меты DataLens
Часть тасков можно запускать вручную.

Спева нужно задать переменные окружения:

`export YT_TOKEN="..."`

`export DL_TOKEN="..."`

Потом запускать сам скрипт.

Собрать все объекты в родительской папке:

`python3 get_entries_in_folder.py --folder_id "avgubsgbykz04" --output_path "//home/taxi-analytics/taxi-bi/datalens-meta/raw/datalens_objects" --expected_rows 1000`

Собрать все отношения для собранных дашбордов:

`python3 get_relations.py --objects_table "//home/taxi-analytics/taxi-bi/datalens-meta/raw/datalens_objects" --relations_table "//home/taxi-analytics/taxi-bi/datalens-meta/raw/relations"`

Собрать информацию о собранных коннекшенах:

`python3 get_connections.py --objects_table "//home/taxi-analytics/taxi-bi/datalens-meta/raw/datalens_objects" --connections_table "//home/taxi-analytics/taxi-bi/datalens-meta/raw/connections"`

После того как RAW слой собран можно позапускать таски из CDM.

Наши параметры в корне `parameters.json`. Можно форкнуть проект себе или использовать свои параметры (как выше) в кубиках и прочих инструментах.

Можно переиспользовать для своих папок и сбора метаданных.
