# Offer-status

## Описание

Генерирует таблицу со статусами офферов. На вход принимает генлоги и process_log (выход от offers-processor).

Не путать с dropped2processlog.

## Пример запуска

```bash
./produce_offer_status \
--yt-proxy arnold \
--yt-token-path ~/.yt/token 
--yt-pool market-testing-indexer \
--yt-process-log //home/market/testing/indexer/stratocaster/mi3/main/20210719_1335/process_log/process_log \ 
--yt-process-log //home/market/testing/indexer/stratocaster/mi3/main/20210719_1335/blue_shard_other_genlog_out/process_log/process_log \
--yt-dropped-offers //home/market/testing/indexer/stratocaster/mi3/main/20210719_1335/dropped_offers \
--yt-genlog //home/market/testing/indexer/stratocaster/mi3/main/20210719_1335/genlog \
--parts-count 16 \
--yt-genlog //home/market/testing/indexer/stratocaster/mi3/main/20210719_1335/genlog_blue_on_white \
--parts-count 8 \
--shops-dat /indexer/market/20210719_1335/input/shops-utf8.dat.report.generated \
--dst-path //home/market/testing/indexer/stratocaster/out/offers_status/20210719_1335
```
