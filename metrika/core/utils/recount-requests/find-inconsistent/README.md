# find-inconsistent-recount-requests

Проверяет, чтобы совпадало количество строк в связанных таблицах рекаунт-реквеста, events.rows == deduplicated_hashes.rows. Выводит ноды, для которых значения отличаются. Ходит по ЗК рекурсивно. Запускать надо с продовой mtcalclog-машины, чтобы был доступ к ClickHouse.

```
drobus@drobus:~/arc/metrika/core/utils/recount-requests/find-inconsistent$ ./find-inconsistent-recount-requests --help
usage: find-inconsistent-recount-requests [-h]
                                          [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                                          [-e {production,testing}] -p PATH
                                          [-m MAX_RECOUNT_REQUEST_PER_LEVEL]

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -e {production,testing}, --environment {production,testing}
                        default testing
  -p PATH, --path PATH  ZK path for check
  -m MAX_RECOUNT_REQUEST_PER_LEVEL, --max_recount_request_per_level MAX_RECOUNT_REQUEST_PER_LEVEL
                        Maximum number of recount requests per node level to
                        scans

For example
./find-inconsistent-recount-requests -e testing -p /metrika-mobile/test_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01 -m 1
```

```
drobus@mtcalclog36i:~$ ./find-inconsistent-recount-requests -e production -p /metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01 -m 1
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_clicklog_events/recount-request-0045388006
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_decoded_crashes/recount-request-0010502780
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_first_events/recount-request-0045387995
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_generic_events_with_history/recount-request-0045388010
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_invalid_events/recount-request-0045387999
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_invalid_imported_events/recount-request-0031930710
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_mtsmart_generic_events/recount-request-0045039342
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_notification_events/recount-request-0045387995
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_open_events/recount-request-0045155157
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_organic_installations/recount-request-0037972438
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_profiles_attributes_counters/recount-request-0029134292
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_profiles_attributes_invalids/recount-request-0029134292
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_profiles_attributes_values/recount-request-0029134292
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_profiles_system_attributes/recount-request-0029134292
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_push_token_events/recount-request-0045387995
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_revenue_events/recount-request-0011769198
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_third_party_clicklog_events/recount-request-0045388006
/metrika-mobile/production_cloud/recount_requests/mobile-clickbuffer-writer/layers/layer01/clickhouse_update_events/recount-request-0045155238
```