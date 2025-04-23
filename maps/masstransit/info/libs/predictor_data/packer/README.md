# Набор тулз для генерации `masstransit_predictor_data.fb`

Процесс генерации flatbuffer-a состоит из трех частей:
- загрузка данных о нитках на YT
- преобразование ниток (сегментация, маппинг геометрии ниток на дорожный граф, определение региона и пр.)
- дамп итоговых таблиц во flatbuffer

### Быстрый старт:
- скачиваем датасет [`yandex-maps-masstransit-data`](http://ecstatic.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions), получаем директорию директорию вида `yandex-maps-masstransit-data_<VERSION>`, далее называемую `<masstransit_data>`
- скачиваем [`coverage`](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions), из него нужен файл `geoid.mms.1`

```bash
$ ./extract_threads_to_yt --input <masstransit_data>/static.fb --output //home/maps/jams/dev/users/<user>/gen_predictor_data_fb/threads
$ ./match_threads_to_road_graph -i //home/maps/jams/dev/users/<user>/gen_predictor_data_fb/threads -o //home/maps/jams/dev/users/<user>/gen_predictor_data_fb --coverage geoid.mms.1
$ ./dump_predictor_data --input <masstransit_data>/static.fb --edges //home/maps/jams/dev/users/<user>/gen_predictor_data_fb/edges --stages //home/maps/jams/dev/users/<user>/gen_predictor_data_fb/stages --regions //home/maps/jams/dev/users/<user>/gen_predictor_data_fb/regions --output masstransit_predictor_data.fb
```

## Загрузка данных о нитках на YT

Загружает данные о нитках из датасета `yandex-maps-masstransit-data` в таблицу на YT.

Бинарник - [`extract_threads_to_yt`](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/packer/extract_threads_to_yt/bin/main.cpp)

| Параметр | Описание |
| -------- | -------- |
| `input` | путь до fb-файла с расписаниями в директории `masstransit_data` (по умолчанию `/var/lib/yandex/maps/ecstatic/data/yandex-maps-masstransit-data/static.fb`) |
| `output` | выходная таблица (будет перезаписана, если существует) |
| `debug` | таблица с нитками, у которых что-то пошло не так. Колонка `error_type` хранит код ошибки `ErrorType`, описанный [здесь](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/packer/extract_threads_to_yt/lib/extract_threads.h) |
| `yt-proxy` | по умолчанию `hahn` |

## Преобразование ниток

Для каждой нитки определяется регион (округлённый до [города](https://doc.yandex-team.ru/lib/libgeobase5/concepts/region-types.html)) - таблица <`thread_id`|`region_id`> записывается в таблицу `regions` <br>
<i> - Стейдж - это кусок нитки между двумя соседними остановками </i><br>
Каждый стейдж разрезается [сегментатором](/arc/trunk/arcadia/maps/masstransit/info/libs/common/segmentation.h) на рёбра, рёбра приматчиваются к дорожному графу <br>
Информация о рёбрах и результат матчинга складывается в таблицу `edges`<br>
Информация о стейджах нитки складывается в таблицу `stages`

Редьюсер лежит непосредственно в [`mk_predictor_data/bin/main.cpp`](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/packer/mk_predictor_data/bin/main.cpp)

Бинарник для запуска руками - [`match_threads_to_road_graph`](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/packer/tools/match_threads_to_road_graph/match_threads_to_road_graph.py)

| Параметр | Описание |
| -------- | -------- |
| `-i`/`input-table` | таблица с нитками (результат выполнения `extract_threads_to_yt`) |
| `-o`/`output-dir` | директория на YT, в которую будут сложены выходные таблицы |
| `coverage` | путь до файла `geoid.mms.1` на локальной машине |
| `geodata` | путь до файла `geodata5.bin` на YT (по умолчанию берется из [`//statbox/statbox-dict-last/geodata5.bin`](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/statbox-dict-last/geodata5.bin)) |
| `-v`/`graph-version` | версия графа, по умолчанию берётся `latest` |
| `graph-folder` | путь до директории с графами на YT (по умолчанию [`//home/maps/graph`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/graph)) |
| `memory-limit` | job memory limit (GB), нужно указать 20, если запускается не в `maps-jams-dev` квоте |

## Дамп во flatbuffer

Читает датасет `yandex-maps-masstransit-data` и таблицы из предыдущего шага и записывает во flatbuffer. Формат данных описан в [`predictor_data`](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/impl/fb/storage.fbs64)

Бинарник - [`dump_predictor_data`](/arc/trunk/arcadia/maps/masstransit/info/mtpredictor/learning/dump_predictor_data/bin/main.cpp)

| Параметр | Описание |
| -------- | -------- |
| `input` | путь до fb-файла с расписаниями в директории `masstransit_data` (по умолчанию `/var/lib/yandex/maps/ecstatic/data/yandex-maps-masstransit-data/static.fb`) |
| `edges` | путь до таблицы `edges` (см. Преобразование ниток) |
| `stages` | путь до таблицы `stages` (см. Преобразование ниток) |
| `regions` | путь до таблицы `regions` (см. Преобразование ниток) |
| `output` | путь до итогового `masstransit_predictor_data.fb` файла |
| `yt-proxy` | по умолчанию `hahn` |
