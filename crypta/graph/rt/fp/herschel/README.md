Подключаемся к qyt очереди

```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
        --proxy 'hahn' \
        consumer create \
        --ignore-in-trimming 0 \
        '//home/crypta/testing/rtsklejka/qyt/sharded_fprints' \
        herschel
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/herschel/offsets'
```

Создаем стейт
```bash
$ yt create --type table \
    --attributes '
        {dynamic=%true;
        schema=[
            {name=Hash;type=uint64;sort_order=ascending;expression=farm_hash(Fp)};
            {name=Fp;type=string;sort_order=ascending};
            {name=State;type=string};
            {name=Codec;type=string}
        ]}' \
    --path //home/crypta/testing/rtsklejka/state/herschel_state

$ yt set '//home/crypta/testing/rtsklejka/state/herschel_state/@min_data_ttl' 0
$ yt set '//home/crypta/testing/rtsklejka/state/herschel_state/@max_data_ttl' 108000000
$ yt set '//home/crypta/testing/rtsklejka/state/herschel_state/@max_data_versions' 1
$ yt set '//home/crypta/testing/rtsklejka/state/herschel_state/@min_data_versions' 0
$ yt mount-table '//home/crypta/testing/rtsklejka/state/herschel_state' --sync
```

```
yt mount-table '//home/crypta/testing/rtsklejka/qyt/sharded_fprints/consumers/herschel/offsets' --sync
```

Создаем стейт (реплики)
