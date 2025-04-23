# simple-mover

Утилита перемещения рекаунт-реквестов внутри ZooKeeper'а. Тестировалась на АппМетрике, <span style="color:red">работоспособность в ВебМетрике не проверялась</span>.

```
usage: simple-mover [-h]
                    [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                    [-e {production,testing}] [-t MAX_TRANSACTION_LENGTH] -f
                    FILE -i INPUT_PREFIX -o OUTPUT_PREFIX

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -e {production,testing}, --environment {production,testing}
                        default testing
  -t MAX_TRANSACTION_LENGTH, --max_transaction_length MAX_TRANSACTION_LENGTH
                        default 1000
  -f FILE, --file FILE  path to local file with absolute recount requests
                        paths to move
  -i INPUT_PREFIX, --input_prefix INPUT_PREFIX
                        recount requests prefix
  -o OUTPUT_PREFIX, --output_prefix OUTPUT_PREFIX
                        path prefix to destination node

For example
./simple-mover -v info -e testing -t 1000 -f local_files_with_recount_requests_paths -i /metrika-mobile/production_cloud -o /metrika-mobile/fuckup_some_date
```

Пример запуска

```
osval@osval:~/monrep/arc/arcadia/metrika/core/utils/recount-requests/simple-mover$ cat file 
/metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415090
/metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415091
/metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415092
/metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415093
/metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415095

osval@osval:~/monrep/arc/arcadia/metrika/core/utils/recount-requests/simple-remover$ ./simple-mover -e testing -f file  -v -o /metrika-mobile/test -i /metrika-mobile/test_cloud
2020-07-23 18:01:49,478	kazoo.client                  	INFO    	Connecting to mtzoo01ft.metrika.yandex.net(2a02:6b8:0:1409:225:90ff:feeb:9636):2181, use_ssl: False
2020-07-23 18:01:49,499	kazoo.client                  	INFO    	Zookeeper connection established, state: CONNECTED
2020-07-23 18:01:49,506	main                          	INFO    	Move /metrika-mobile/test_cloud/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415090 to /metrika-mobile/test/recount_requests/columnar-appender-mobile/layers/layer01/columnar_appender_mobile_logs/recount-request-0011415090
2020-07-23 18:01:49,516	main                          	INFO    	RR data H4sIAAAAAAAAA82Ry26DMBBFf6WaNaG2scPjM7qtopELk4KwMbGHtBHi3+t23XVVae7mLu450uwQ6bZR4gTdDgNd7eYYutcdYvjIXVMXkDhE+ulWyyN00Ae3+cVGtOtKy0ARfXibHKEL7+n5hdYQGZVQAkWNqkKp0eQzWDWtMq1GoSulmyYHpWmNkWfZGBxo2FY39Tbz0NlH3tVQwBhSNgLPvXV9Jgg5c+mJ4zTb8mEz/7NciOEo/ouguv4ueCmgH7dlxmn4c0m608LIk8+fhO/Vk6hPqnqSdWfOnWqz3XF8AQgy1t4OAgAA
```
