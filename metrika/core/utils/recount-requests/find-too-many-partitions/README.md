# find-too-many-partitions

Проверяет, чтобы в таблице events было не более 1 партиции в рамках одного рекаунт-реквеста. Выводит ноды, для которых партиций больше 1, выводит кол-во партиций для разных типов событий ('sdk'/'import_api'). Ходит по ЗК рекурсивно. Запускать надо с продовой mtcalclog-машины, чтобы был доступ к ClickHouse. Реквесты с unique_events вместо events + deduplicated_hashes пропускаются.

```
pperestoronin@mtcalclog36i:~$ ./find-too-many-partitions-recount-requests --help
usage: find-too-many-partitions-recount-requests [-h]
                                                 [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                                                 [-e {production,testing}]
                                                 [-z ZKGROUP] -p PATH
                                                 [-m MAX_RECOUNT_REQUEST_PER_LEVEL]

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -e {production,testing}, --environment {production,testing}
                        default testing
  -z ZKGROUP, --zkgroup ZKGROUP
                        default common-proxy
  -p PATH, --path PATH  ZK path for check
  -m MAX_RECOUNT_REQUEST_PER_LEVEL, --max_recount_request_per_level MAX_RECOUNT_REQUEST_PER_LEVEL
                        Maximum number of recount requests per node level to
                        scans

For example
./find-too-many-partitions-recount-requests -e testing -p /metrika-mobile/test_cloud/recount_requests/mobile-giga-events-writer/layers/layer01 -m 1
```

```
pperestoronin@mtcalclog36i:~$ ./find-too-many-partitions-recount-requests -e production -p /metrika-mobile/production_cloud/recount_requests/mobile-giga-events-writer/layers/layer01 -m 100
Processed 18
```
