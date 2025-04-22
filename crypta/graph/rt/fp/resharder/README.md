Работа с таблицами очереди.

```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/iva/yabs-rt_bs-event-log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/man/yabs-rt_bs-event-log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/myt/yabs-rt_bs-event-log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/sas/yabs-rt_bs-event-log/offsets'

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/vla/yabs-rt_bs-event-log/offsets'
```

------

```bash
$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    queue create '//home/crypta/testing/rtsklejka/qyt/sharded_fprints' \
    --shards 128 \
    --medium default \
    --max-ttl 3h

$ ./ads/bsyeti/big_rt/cli/big_rt_cli \
    --proxy 'hahn' \
    queue trim '//home/crypta/testing/rtsklejka/qyt/sharded_fprints' \
    --ignore-consumers
```

```
ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/consuming_systems/iva/yabs-rt_bs-event-log/offsets' --recursive ;
ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/consuming_systems/man/yabs-rt_bs-event-log/offsets' --recursive ;
ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/consuming_systems/myt/yabs-rt_bs-event-log/offsets' --recursive ;
ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/consuming_systems/sas/yabs-rt_bs-event-log/offsets' --recursive ;
ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/consuming_systems/vla/yabs-rt_bs-event-log/offsets' --recursive ;

./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/iva/yabs-rt_bs-event-log/offsets' ;
./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/man/yabs-rt_bs-event-log/offsets' ;
./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/myt/yabs-rt_bs-event-log/offsets' ;
./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/sas/yabs-rt_bs-event-log/offsets' ;
./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' offsets_table create '//home/crypta/testing/rtsklejka/consuming_systems/vla/yabs-rt_bs-event-log/offsets' ;

ya tool yt --proxy hahn remove '//home/crypta/testing/rtsklejka/qyt/sharded_fprints' --recursive ;
./ads/bsyeti/big_rt/cli/big_rt_cli --proxy 'hahn' queue create '//home/crypta/testing/rtsklejka/qyt/sharded_fprints' --shards 128 --medium default --max-ttl 3h ;
```
