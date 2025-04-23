# delete-recount-requests

Утилита удаления рекаунт-реквестов из ZooKeeper'а. Тестировалась на АппМетрике, <span style="color:red">работоспособность в ВебМетрике не проверялась</span>. Скорее всего не заработает из-за различия в формате путей. Репозиторий общий, как говорится.

```
drobus@drobus:~/arc/metrika/core/utils/recount-requests/delete$ ./delete-recount-requests --help
usage: delete-recount-requests [-h]
                               [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                               [-e {production,testing}]
                               [-t MAX_TRANSACTION_LENGTH] -p PATH

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -e {production,testing}, --environment {production,testing}
                        default testing
  -t MAX_TRANSACTION_LENGTH, --max_transaction_length MAX_TRANSACTION_LENGTH
                        default 1000
  -p PATH, --path PATH  ZK path for delete

For example
./delete-recount-requests -v info -e testing -t 1000 -p /metrika-mobile/test_cloud/recount_requests/mobile-statbox-events-writer/layers
```

Пример запуска
```
drobus@drobus:~/arc/metrika/core/utils/recount-requests/delete$ ./delete-recount-requests -v info -e testing -t 1000 -p /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers
[2020/03/24-17:13:44][kazoo.client][INFO]: Connecting to 2a02:6b8:0:817:225:90ff:feeb:9460:2181, use_ssl: False
[2020/03/24-17:13:45][kazoo.client][INFO]: Zookeeper connection established, state: CONNECTED
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer02/clickhouse_mtsmart_client_events
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer02/clickhouse_mtsmart_statbox_events
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer02/clickhouse_client_events
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer01/clickhouse_mtsmart_client_events
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer01/clickhouse_mtsmart_statbox_events
[2020/03/24-17:13:45][main][INFO]: Deleting /metrika-mobile/test_cloud/recount_requests/mobile-massive-destinations-writer/layers/layer01/clickhouse_client_events
[2020/03/24-17:13:45][main][INFO]: Delete done
[2020/03/24-17:13:45][kazoo.client][INFO]: Closing connection to 2a02:6b8:0:817:225:90ff:feeb:9460:2181
[2020/03/24-17:13:45][kazoo.client][INFO]: Zookeeper session lost, state: CLOSED
```