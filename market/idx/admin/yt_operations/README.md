Консольная грепалка операций YT

```
bzz13@dev-idx01vd:~/arcadia/market/idx/admin/yt_operations$ ya make -tA
------- [TS] $(B)/result.log
Total 3 suites:
    3 - GOOD
Total 5 tests:
    5 - GOOD
Ok


bzz13@dev-idx01vd:~/arcadia/market/idx/admin/yt_operations$ ./bin/yt_operations --help
Usage: yt_operations [OPTIONS]

Options:
  -h, --help            show this help message and exit
  --yt-token-path=YT_TOKEN_PATH
                        yt token path
  --yt-proxy=YT_PROXY   yt proxy to cluster (like hahn)
  --yt-pool=YT_POOL     yt pool on cluster for operations collecting
  --from=FROM_TIME      define date time for operations beginning in format
                        "%Y%m%d_%H%M" (20200206_1141)
  --to=TO_TIME          define datetime for operations ending in format
                        "%Y%m%d_%H%M" (20200206_1241)
  --limit=MIN_JOB_COUNT
                        minimum job count for filter (defualt 2500)


bzz13@dev-idx01vd:~/arcadia/market/idx/admin/yt_operations$ scp ./bin/yt_operations mi01ht.market.yandex.net:/home/bzz13/
yt_operations                                                                       100%   34MB  33.7MB/s   00:01


bzz13@dev-idx01vd:~/arcadia/market/idx/admin/yt_operations$ ssh bzz13@mi01ht.market.yandex.net \
> '/home/bzz13/yt_operations --yt-token-path=/etc/datasources/yt-market-indexer --yt-proxy=arnold --yt-pool=market-production-indexer-white --from=20200206_1742 --to=20200206_1917'


2020-02-07 14:55:05,300 - yt_operations - INFO - [
    {
        "finish_time": "2020-02-06T19:00:19.094265Z",
        "id": "db939df9-320d664c-41103e8-76da76fc",
        "start_time": "2020-02-06T18:54:13.676791Z",
        "title": "reducer:NMarket::NOR3::TGenerationCreatorReducer",
        "total": 2321,
        "url": "https://yt.yandex-team.ru/arnold/operations/db939df9-320d664c-41103e8-76da76fc/details",
        "user": "robot-mrkt-idx-prod"
    },
    {
        "finish_time": "2020-02-06T19:17:08.291907Z",
        "id": "172a77d4-10f5a17a-41103e8-2d250196",
        "start_time": "2020-02-06T19:15:03.938048Z",
        "title": "NMarket::NOR3::TPictureReducer<true>",
        "total": 1370,
        "url": "https://yt.yandex-team.ru/arnold/operations/172a77d4-10f5a17a-41103e8-2d250196/details",
        "user": "robot-mrkt-idx-prod"
    },
    {
        "finish_time": "2020-02-06T19:23:50.652372Z",
        "id": "94718a-567b1363-41103e8-f5cd90f7",
        "start_time": "2020-02-06T19:00:55.059468Z",
        "title": "mapper:TErfMapper reducer:TWebErfDataByUrlReducer",
        "total": 880,
        "url": "https://yt.yandex-team.ru/arnold/operations/94718a-567b1363-41103e8-f5cd90f7/details",
        "user": "robot-mrkt-idx-prod"
    },
    {
        "finish_time": "2020-02-06T19:06:19.457620Z",
        "id": "9881d336-cf8cd2d6-41103e8-d22bd203",
        "start_time": "2020-02-06T19:03:32.633685Z",
        "title": "YQL operation (5e3c62fe68a6f53ca65c02f5 by robot-mrkt-idx-prod)",
        "total": 827,
        "url": "https://yt.yandex-team.ru/arnold/operations/9881d336-cf8cd2d6-41103e8-d22bd203/details",
        "user": "robot-mrkt-idx-prod"
    }
]
```
