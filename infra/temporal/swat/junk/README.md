### ./maru
```sh
git clone https://github.com/temporalio/maru.git
```
adapted to Arcadia and using infra/temporal/swat/client.

To run benchmarking worker:
```sh
$ pwd
/Users/romanovich/sources/arcadia/infra/temporal/swat/junk/maru/worker/cmd
$ TOKEN=AQAD-XXX NAMESPACE=bench NAMESPACE_RETENTION=1 FRONTEND_ADDRESS=dev-temporal.in.yandex.net:7233 NUM_DECISION_POLLERS=10 ./cmd
```

Benchmarking worker in Nanny:
https://nanny.yandex-team.ru/ui/#/services/catalog/dev_temporal_bench_worker/
https://grafana.yandex-team.ru/d/0pIsD-t7z/temporal-bench-worker?orgId=1&from=now-5m&to=now&refresh=5s
https://yasm.yandex-team.ru/template/panel/dbaas_mysql_metrics/cid=mdbjtu5cdeks7l9op0ed
```sh
$ ya make --target-platform=default-linux-x86_64 -DCGO_ENABLED=0
$ ya upload ./worker
```

To start benchmark:
```sh
$ export TEMPORAL_TOKEN=AQAD-XXX
$ pwd
/Users/romanovich/sources/arcadia/infra/temporal/swat/tctl
$ ./tctl --address dev-temporal.in.yandex.net:7233 --ns bench wf start --tq temporal-bench --wt bench-workflow --wtt 5 --et 1800 \
--if /Users/romanovich/sources/arcadia/infra/temporal/swat/junk/maru/scenarios/basic-test.json --wid 1
```

Moar details: https://github.com/temporalio/maru/
