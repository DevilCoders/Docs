# service_reducer

Программа предназанчена для конвертации yt таблиц генлога в таблицу сервисных офферов.
Под таблицами генлога понимается выхлоп offers-processor'а.
На выходе должны получить:
1) строки с отношением бизнес (главного) и сервисных (схлопнутых) офферов. В строке отношение 1 к 1.
2) генлог таблицы с бизнес-офферами.

Пример запуска:
```shell
./service_reducer \
--yt-proxy arnold \
--yt-genlog-input-dir //home/market/testing/indexer/users/20210805_1658/genlog_blue_on_white \
--yt-collapse-genlog-dir //home/market/testing/indexer/users/20210805_1658/new_collapse_genlog \
--yt-filtered-genlog-dir //home/market/testing/indexer/users/20210805_1658/new_filtered_genlog \
--yt-relation-output-dir //home/market/testing/indexer/users/20210805_1658/new_relations \
--yt-genlog-output-dir //home/market/testing/indexer/users/20210805_1658/new_business_genlog \
--currency-rates-path currency_rates.xml \
--generation 20210805_1658
```
