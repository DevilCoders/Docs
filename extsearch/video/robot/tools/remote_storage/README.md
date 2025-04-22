# Утилита для проверки подключения к Remote Storage и получения из него данных по документам видео

## Запуск

* `INDEX_VERSION` - версия индекса (timestamp)
* `PATH_TO_INDEX` - путь до каталога с маппингами, можно либо выкачать ресурс `VIDEO_SEARCH_DATABASE` для соответствующего шарда, либо выкачать бинарником `extsearch/video/robot/docbase/remote_storage/index_builder`.
* `PATH_TO_SHARD_RS_CONFIG` - конфигурация remote storage для данного шарда. Чтобы достать файл, можно выкачать ресурс `CAJUPER_VIDEO_PLATINUM_CHUNKS_CONFIGS_BUNDLE`. Нужно не забыть поднять таймауты в этом конфиге.
* `DOC_ID` (только для get-режима) - проверяемый документ.
* `PORTION_SIZE` (только для fetch-режима) - размер порции, которая будет скачана из remote storage.

### Проверка одного документа (Get)

`./rs_check_wad --version INDEX_VERSION --index-name PATH_TO_INDEX/index -i PATH_TO_SHARD_RS_CONFIG get --doc-id DOC_ID`

### Проверка всех документов (Fetch)

`./rs_check_wad --version INDEX_VERSION --index-name PATH_TO_INDEX/index -i PATH_TO_SHARD_RS_CONFIG fetch --portion-size PORTION_SIZE`

## Ссылки на похожие утилиты

* https://a.yandex-team.ru/arc/trunk/arcadia/search/base/blob_storage/cli/main.cpp
* https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/images/tools/shard_dumper/arcrs.cpp#L176
