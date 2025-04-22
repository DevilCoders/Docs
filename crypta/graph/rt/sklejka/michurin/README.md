Для того чтобы michurin работал надо

1. Добавить его в качестве конзьюмера в очередь
```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
        --proxy 'hahn' \
        consumer create \
        --ignore-in-trimming 0 \
        '//home/crypta/testing/rtsklejka/qyt/sharded_events' \
        michurin
```

1. Завести offsets таблицу для него
```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/rtsklejka/consuming_systems/michurin/offsets'
```

1. Завести state таблицу и примонтировать её

```bash
$ ya tool yt create --type table \
    --attributes '{dynamic=%true;schema=[{name=Id;type=string;sort_order=ascending};{name=State;type=string};{name=Codec;type=string}]}' \
    --path //home/crypta/testing/rtsklejka/state/michurin_state

$ ya tool yt mount-table '//home/crypta/testing/rtsklejka/state/michurin_state'
```
