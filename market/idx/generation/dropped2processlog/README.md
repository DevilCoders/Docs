# dropped2processlog

## O программе

 - Цель программы выгружать в динамическую таблицу process_log информацию о оферах, которые были выкинуты из индекса благодаря механике проекта "Умный индекс"
 - Данная информация необходима партнерке для отображения магазинам о подобных скритиях.
 - Источником данных для данной программв является статическая таблица {indexation_dir}}//mi3/main/{GENERATION}/dropped_offers
 - Вызов данной программы происходит в процессе сборки поколения, после работы main-idx

## Пример запуска

```
./dropped2processlog \
    --yt-proxy hahn \
    --yt-input-table //home/market/production/indexer/stratocaster/mi3/main/last_complete/dropped_offers \
    --generation-name {GENERATION} \
    --yt-output-table //home/market/production/indexer/stratocaster/out/process_log \
    --yt-dynamic-bundle {bundle} \
    --yt-token-path {token_path}
```

```
/usr/lib/yandex/dropped2processlog \
    --generation-name 20210415_1415 \
    --process-log-auto-compaction-period-days 1 \
    --process-log-ttl-days 7 \
    --yt-input-table //home/market/production/indexer/stratocaster/mi3/main/last_complete/dropped_offers \
    --yt-output-table //home/market/production/indexer/stratocaster/out/logs/process_log.v2 \
    --yt-pool market-production-indexer-white \
    --yt-proxy hahn.yt.yandex.net \
    --yt-token-path /etc/datasources/yt-market-indexer \
    --do-bulk-insert
```
