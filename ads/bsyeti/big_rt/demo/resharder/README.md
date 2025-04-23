Создаем консьюмер в lb:

```bash
$ logbroker -s logbroker schema create consumer /crypta/test/graph/demo_resharder/consumer
$ logbroker -s logbroker schema create read-rule \
    -t /crypta/prod/graph/soup \
    -c /crypta/test/graph/demo_resharder/consumer \
    --all-original
$ logbroker -s logbroker permissions grant \
    --path /crypta/test/graph/demo_resharder/consumer \
    --subject 2017217@tvm \
    --permissions ReadAsConsumer
```

Создаем таблицы для работы решардера:

```bash
$ # QYT шардированная очередь
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    queue create '//home/crypta/demo_resharder/qyt/sharded_events' \
    --shards 64 \
    --medium default \
    --max-ttl 30m
$ # Технические таблицы для работы с оффсетами
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    offsets_table create '//home/crypta/demo_resharder/cs/sas_soup_log/offsets'
```
