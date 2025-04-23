# service_mapping_dumper64

На вход принимает шардированные таблицы всех отношений сервисных и бизнес офферов. Дампит 2 файла.

Сливает все исходные таблицы в одну и сортирует по business_id, чтобы не хранить всю таблицу в памяти.

### feed_id-мастера (который содержит бизнес офер) для каждого offer_id для бизнеса.

```json
{
  business_id_1: {
    yabs_offer_id_1: XXX,
    yabs_offer_id_2: YYY,
  },
  business_id_2: {
    yabs_offer_id_n: WWW,
    yabs_offer_id_m: VVV,
  }
}
```

### Маппинг ware_md5 сервисных офферов в ware_md5 бизнес офферов.

Описание алгоритма:
https://st.yandex-team.ru/MARKETINDEXER-45419#6218fb8cd310ce0fd778a4aa

Пример запуска:
```shell
./service_mapping_dumper64 \
--yt-proxy arnold \
--yt-token-path ~/.yt/testing_token \
--yt-input-dir //home/market/testing/indexer/users/reduced \
--yt-output-table //home/market/testing/indexer/users/layer_table \
--output-path ~/fb/
```
