# Coroner

Linux netconsole server

## Documentation
[Coroner](https://wiki.yandex-team.ru/kernel/#coroner)
[YT](https://docs.yandex-team.ru/yt/overview/about_YT)
[CHYT](https://docs.yandex-team.ru/yt/description/chyt/about_chyt)
[DataLens](https://datalens.yandex-team.ru/docs/)

## Links
[ABC service](https://abc.yandex-team.ru/services/coroner/)
[Nanny service](https://nanny.yandex-team.ru/ui/#/services/catalog/coroner_vla/)
[Nanny service test](https://nanny.yandex-team.ru/ui/#/services/catalog/test_coroner)
[TestEnv](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/CORONER/history)
[Datalens](https://datalens.yandex-team.ru/sod7ifevy55yn-coroner)
[YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/coroner)
[CHYT](https://yt.yandex-team.ru/hahn/operations/62beea38-a4f53945-3fe03e8-4b75a499/details)

## Monitoring
[Yasm Tree](https://yasm.yandex-team.ru/menu/RTCSRE/Coroner)
[Solomon CHYT](https://monitoring.yandex-team.ru/projects/yt/dashboards/mondiesv18abvn6min0e?p.cluster=hahn&p.service=clickhouse&p.operation_alias=ch_coroner&p.cookie=Aggr&range=1d&refresh=60)
[Hostman client side](http://hm-prestable.in.yandex.net:8998/units/yandex-coroner)
[Orly client side](https://a.yandex-team.ru/arc_vcs/infra/orly/rules/system-service-yandex-coroner.yaml)

## Prepare
```
yt clickhouse start-clique --proxy hahn --instance-count 2 --alias *ch_coroner --spec '{pool=rtcsysdev-pool; title="CHYT for coroner"; acl=[{subjects=["idm-group:112397"];action=allow;permissions=["read";"manage"];};{subjects=["robot-rtc-builder"];action=allow;permissions=[read];}]}' --cpu-limit 4 --abort-existing --clickhouse-config '{yt={subquery={max_data_weight_per_subquery=1000000000000}}}'
```
## Testing
```
./cmd/coroner/coroner -ddd  run --http_port 8080 --udp_port 6667
cat test/sas1-3333.search.yandex.net-2020-04-22.log | nc -q 5 -u -6 localhost 6667
```

## How It Works

## TODO coroner
* add alerts
* fix problem with 65535 bytes
* add logging
* yt batchSize, maybe add push every 5 min
* remove old repo arcadia/infra/coroner_server
* write coronerctl based on YT and replace arcadia/kernel/tools/coroner
* move upload.go to coronerctl
* rename testenv task coroner -> yandex-coroner
* **parser** get oops_id from oops msg `---[ end trace %016llx ]---`
* **blocked for more than** not detect comm
* write_succ is zero
* YTStorage error on writing oops: call c1ae28c9-ec43ea18-f34356b5-9c3615d1 failed: error starting upload to table //tmp/coroner/oops: request retries failed: read-only mode is active
YTStorage error on writing oops: call c1ae28c9-ec43ea18-f34356b5-9c3615d1 failed: error starting upload to table //tmp/coroner/oops: request retries failed: read-only mode is active
* problems with write
YTStorage error on writing oops: call 9489376a-c4b9cef-5e92139f-8085b931 failed: put "http://sas0-1878-proxy-hahn.sas.yp-c.yandex.net/api/v4/write_table": read tcp [2a02:6b8:c0f:1818:0:475d:9d12:0]:51730->[2a02:6b8:c21:2123:0:4397:1335:0]:80: read: connection reset by peer
YTStorage error on writing oops: call 9489376a-c4b9cef-5e92139f-8085b931 failed: put "http://sas0-1878-proxy-hahn.sas.yp-c.yandex.net/api/v4/write_table": read tcp [2a02:6b8:c0f:1818:0:475d:9d12:0]:51730->[2a02:6b8:c21:2123:0:4397:1335:0]:80: read: connection reset by peer
* YTStorage error on writing oops: call 69f196fe-f342074a-34f6c4b5-dffe68d7 failed: error validating column "message": not a valid utf8 string


ERROR: YTStorage error on writing oops: call 8bdc6ef7-714944fc-193dfaaa-35018c01 failed: error validating column "message": not a valid utf8 string
ERROR: YTStorage error on writing oops: call 8bdc6ef7-714944fc-193dfaaa-35018c01 failed: error validating column "message": not a valid utf8 string

