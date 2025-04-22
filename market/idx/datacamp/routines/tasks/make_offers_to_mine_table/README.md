# make_offers_to_mine_table

Создает таблицу офферов для force перемайнинга: https://docs.yandex-team.ru/market-datacamp/components/routines/admin#post-/mine?sync

## Пример запуска:
```
./tasks_runner --make-offers-to-mine-table -p arnold --token ~/.yt/token -i //home/market/testing/indexer/datacamp/united/service_offers -o //tmp/s7and/testing --from-ts 1644494400
```

## Параметры запуска:
```
  {-i|--input} Путь к таблице с сервисными офферами
  {-o|--output} Выходная таблица
  {-p|--proxy} Yt Proxy
  {--token} Yt Token Path
  {--from-ts} таймстемп в секундах: оффера с какого времени записать в таблицу
  {--to-ts} таймстемп в секундах: оффера до какого времени записать в таблицу
  {--from-version} оффера с версией манера больше этой запишутся в таблицу
  {--to-version} оффера с версией манера меньше этой запишутся в таблицу
  {--err-table} Yt stderr table path
  {--pool} Yt pool

```

Для запуска обязательно указвать input, output и хотя бы один из параметров фильтрации from-ts, to-ts, from-version или to-version.

## Сортировка выходной таблицы:  
Выходная таблица будет отсортирована по business_id, shop_sku, shop_id, warehouse_id.
