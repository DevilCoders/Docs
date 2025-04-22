# new_service_reducer

Программа предназанчена для конвертации yt таблиц генлога в таблицы бизнес офферов.
Под таблицами генлога понимается выхлоп offers-processor'а.

Пример запуска:

```shell
./service_reducer \
--yt-proxy arnold \
--medium ssd_blobs \
--generation 20210924_1028 \
--yt-collapse-genlog-dir //home/market/testing/indexer/users/20210924_1028/genlog \
--yt-genlog-output-dir //home/market/testing/indexer/users/20210924_1028/genlog_business
```

