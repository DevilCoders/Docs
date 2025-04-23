Работа с таблицами очереди.

```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    queue create '//home/crypta/rtsklejka/qyt/sharded_events' \
    --shards 512 \
    --medium default \
    --max-ttl 3h

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    offsets_table create '//home/crypta/rtsklejka/consuming_systems/sas/soup_log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    offsets_table create '//home/crypta/rtsklejka/consuming_systems/man/soup_log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'zeno' \
    queue trim '//home/crypta/rtsklejka/qyt/sharded_events' \
    --ignore-consumers
```

------

```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    queue create '//home/crypta/testing/rtsklejka/qyt/sharded_events' \
    --shards 512 \
    --medium default \
    --max-ttl 3h

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/sas/soup_log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/man/soup_log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    queue trim '//home/crypta/testing/rtsklejka/qyt/sharded_events' \
    --ignore-consumers
```
