### How to create dynamic queue

Use [big_rt_cli](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/big_rt/cli)

```text
YT_PROXY=arnold ./big_rt_cli queue create //home/search-runtime/sankear/queue --shards 8 --max-ttl 1d
```

### How to add consumer to dynamic queue

```text
YT_PROXY=arnold ./big_rt_cli consumer create //home/search-runtime/sankear/queue plutonium_worker --ignore-in-trimming 0
```

### How to set allowed proto types for dynamic queue

```text
cat t.json
["NPlutonium::NExamples::TExampleErf"]

YT_PROXY=arnold yt set //home/search-runtime/sankear/queue/@allowed_proto_types --format json <t.json
```

