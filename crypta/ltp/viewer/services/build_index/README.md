Автообновление индекса LTP 
========================================================================
Регулярный процесс обновления индекса для смотрелки Long Term Profile: https://search.crypta.yandex-team.ru/?query=history

Внимание: при обновлении индекса есть риск исчерпать ssd квоту crypta-graph, следить за ней можно тут: https://yt.yandex-team.ru/hahn/accounts/general?filter=crypta-graph&medium=ssd_blobs

Подробности [CRYPTA-15807](https://st.yandex-team.ru/CRYPTA-15807)

### Запуск

```bash
$ ./crypta/ltp/viewer/services/build_index --help
usage: main [-h] [--index-path INDEX_PATH] [--tmp-index-path TMP_INDEX_PATH]
            [--start-date START_DATE] [--end-date END_DATE]
            [--min-history-date MIN_HISTORY_DATE]

LTP index update

optional arguments:
  -h, --help            show this help message and exit
  --index-path INDEX_PATH
                        YT path to ssd dynamic index. Example:
                        //home/crypta/{env}/portal/ltp/ids_index_dynamic_ssd
  --tmp-index-path TMP_INDEX_PATH
                        YT path to tmp hdd static table. Example: 
                        //home/crypta/{env}/portal/ltp/ids_index_hdd
  --start-date START_DATE
                        Date for start of update period. Example: 2021-12-12
  --end-date END_DATE   Date for end of update period. Example: 2021-12-13
  --min-history-date MIN_HISTORY_DATE
                        Date for cleanup history. Example: 2021-12-01

# в атрибутах хранятся границы (включительно) временного диапозона индекса (по умолчанию последние 180 дней)
$ yt get //<index path>/@_min_history_date
$ yt get //<index path>/@_max_history_date

# Примеры запуска:

# без параметров автоматически вычислится период для добавления новых данных относительно текущего индекса 
$ ENV_TYPE=development YT_TOKEN=<robot-crypta> ./crypta/ltp/viewer/services/build_index/bin/main

# можно указать пути для текущего ssd индекса и временной таблицы для мерджа
$ ENV_TYPE=development YT_TOKEN=<robot-crypta> ./crypta/ltp/viewer/services/build_index/bin/main \
  --index-path <//path/to/index> \
  --tmp-index-path <//path/to/tmp/index>

# также можно указать период, за который нужно добавить данные для индекса,
# в том числе можно расширить текущий временной диапозон индекса
$ ENV_TYPE=development YT_TOKEN=<robot-crypta> ./crypta/ltp/viewer/services/build_index/bin/main \
    --start-date 2021-12-12 \
    --end-date 2021-12-15 \
    --min-history-date 2021-06-12
    
```


### Как заменить таблицу индекса
```python
import yt.wrapper as yt

client = yt.YtClient(proxy="hahn.yt.yandex.net", token="<token>")

current_index_path = "<index_path>"
new_index_path = "<new_data>"
schema = client.get_attribute(current_index_path, "schema")
optimize_for = client.get_attribute(current_index_path, "optimize_for", default="lookup")

min_history_date = "<iso-date>" or client.get_attribute(current_index_path, "_min_history_date")
max_history_date = "<iso-date>" or client.get_attribute(current_index_path, "_max_history_date")

# make blocks smaller (required for real-time lookups)
client.run_sort(
    new_index_path, 
    yt.TablePath(new_index_path, attributes={"account": "crypta-graph", "schema": schema, "optimize_for": optimize_for}),
    sort_by=["id", "id_type"],
    spec={
        "job_io": {"table_writer": {"block_size": 256 * 2**10, "desired_chunk_size": 100 * 2**20}},
        "force_transform": True
})

# Make table dynamic
client.alter_table(new_index_path, dynamic=True)

# Move to SSD
client.set_attribute(new_index_path, "primary_medium", "ssd_blobs")

client.set_attribute(new_index_path, "_min_history_date", min_history_date)
client.set_attribute(new_index_path, "_max_history_date", max_history_date)

client.mount_table(new_index_path, sync=True)

# Move to portal path 
client.move(new_index_path, current_index_path, force=True)
```
