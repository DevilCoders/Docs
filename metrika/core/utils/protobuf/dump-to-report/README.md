# dump-to-report

Если протобуф заслать в тестинг, то он осядет текстовым дампом в https://report.appmetrica.mtmobproxy-test.yandex.net:8443/debug-reports/. Утилита предназначена для конвертации дампа в бинарный протобуф, в message [Report](https://a.yandex-team.ru/arc/trunk/arcadia/metrika/core/libs/appmetrica/protos/messages/report.proto?rev=4242005#L6).

```
./dump-to-report --help
usage: dump-to-report [-h]
                      [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                      -i INPUT_DUMP_FILE -o OUTPUT_REPORT_FILE
                      [--verbose-input] [--verbose-output]

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -i INPUT_DUMP_FILE, --input-dump-file INPUT_DUMP_FILE
                        dump file after mobile-proxy from debug-reports folder
  -o OUTPUT_REPORT_FILE, --output-report-file OUTPUT_REPORT_FILE
                        protobuf Report message
  --verbose-input       with -v info
  --verbose-output      with -v info

For example
./dump-to-report -i ~/992.analytics_sdk_report -o ~/992.analytics_sdk_report.proto
```

Пример запуска
```
drobus@drobus:~/arc/metrika/core/utils/protobuf/dump-to-report$ ./dump-to-report -i ~/1534.analytics_sdk_report -o ~/1534.analytics_sdk_report.proto --verbose-output -v info
[2020/09/12-23:45:56][main][INFO]: output report =
message: "\032\324\003\010\200\310\257\240%\022\025\n\n\010\364\242\363\372\005\020\340\250\001\022\005be_BY(\001\032\264\003\010\006\020\003\030\004\"\017extensions_list*\360\002{\"extensions\":{\"com.apple.widget-extension\":[\"ru.yandex.mobile.MetricaSample.MetricaSampleToday\"],\"com.apple.photo-editing\":[\"ru.yandex.mobile.MetricaSample.MetricaSamplePhoto\"],\"com.apple.keyboard-service\":[\"ru.yandex.mobile.MetricaSample.MetricaSampleKeyboard\"]},\"own_type\":{\"extension\":\"com.apple.widget-extension\"},\"app_bundle_id\":\"ru.yandex.mobile.MetricaSample\"}:\036\030\001\"\032CTRadioAccessTechnologyLTEh\001x\001\200\001\006\210\001\002\"H\n f384abdf9f554bcca4e28f108ff90046\022$31B24140-CCA8-4871-8EE8-249E023CE735R\013\010\201\002\020\004\032\004Life"
client_ip: ""
device_id_hash: 0
request_parameters {
  uuid: "f384abdf9f554bcca4e28f108ff90046"
  device_id: "31B24140-CCA8-4871-8EE8-249E023CE735"
  app_platform: "iOS"
  app_version_name: "3120"
  app_id: "ru.yandex.mobile.MetricaSample.MetricaSampleToday"
  manufacturer: "Apple"
  model: "iPhone12,8"
  os_version: "13.6.1"
  screen_width: 375
  screen_height: 667
  screen_dpi: 326
  scale_factor: 2.0
  locale: "be_BY"
  device_type: PHONE
  is_rooted: false
  app_build_number: 0
  ifv: "31B24140-CCA8-4871-8EE8-249E023CE735"
  api_key_128: "20799a27-fa80-4b36-b2db-0f8141f24180"
  ifa: "51DBDBDE-7526-43EF-AF61-E51D740853FA"
  app_framework: NATIVE
  os_api_level: 13
  kit_build_type: STATIC
  kit_build_number: 0
  app_debuggable: false
  limit_ad_tracking: false
  is_request_encrypted: false
  kit_version_name: "3.12.0"
  request_id: 1
  attribution_id: 1
}
receive_time {
  timestamp: 1599727962
  time_zone: 10800
  obtained_before_first_synchronization: true
}
client_port: 0
send_time {
  timestamp: 1599727962
  time_zone: 10800
  obtained_before_first_synchronization: true
}
client_ip_hash: 0
```
