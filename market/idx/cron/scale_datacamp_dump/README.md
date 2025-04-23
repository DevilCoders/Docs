# scale_datacamp_dump

Программа предназанчена для размножения моноцветных выгрузок хранилища.


Пример запуска:
```shell
market/idx/cron/scale_datacamp_dump/bin/scale_datacamp_dump \
--params-yt-proxy arnold \
--input-table //home/market/production/indexer/datacamp/united/white_out/recent \
--output-table //home/market/development/indexer/$USER/scale_datacamp_dump_table
```
