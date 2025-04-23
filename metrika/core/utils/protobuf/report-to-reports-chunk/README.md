# report-to-reports-chunk

Утилита складывает протобуфы [Report](https://a.yandex-team.ru/arc/trunk/arcadia/metrika/core/libs/appmetrica/protos/messages/report.proto?rev=4242005#L6) в чанк [ReportsChunk](https://a.yandex-team.ru/arc/trunk/arcadia/metrika/core/libs/appmetrica/protos/messages/report.proto?rev=4242005#L20).

```
./report-to-reports-chunk --helpusage: report-to-reports-chunk [-h]
                               [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                               -i INPUT_REPORT_FILES [INPUT_REPORT_FILES ...]
                               -o OUTPUT_REPORTS_CHUNK_FILE [--verbose-input]
                               [--verbose-output]

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -i INPUT_REPORT_FILES [INPUT_REPORT_FILES ...], --input-report-file INPUT_REPORT_FILES [INPUT_REPORT_FILES ...]
                        one or more protobuf Report message
  -o OUTPUT_REPORTS_CHUNK_FILE, --output-reports-chunk-file OUTPUT_REPORTS_CHUNK_FILE
                        protobuf ReportsChunk message
  --verbose-input       with -v info
  --verbose-output      with -v info

For example
./report-to-reports-chunk -i ~/1504.analytics_sdk_report.proto ~/1534.analytics_sdk_report.proto -o ~/analytics_sdk_reports-chunk.proto -v info --verbose-output
```

Пример запуска
```
drobus@drobus:~/arc/metrika/core/utils/protobuf/report-to-reports-chunk$ ./report-to-reports-chunk -i ~/1504.analytics_sdk_report.proto ~/1534.analytics_sdk_report.proto -o ~/analytics_sdk_reports-chunk.proto -v info --verbose-output
[2020/09/13-00:23:00][main][INFO]: Processing /home/drobus/1504.analytics_sdk_report.proto
[2020/09/13-00:23:00][main][INFO]: Processing /home/drobus/1534.analytics_sdk_report.proto
[2020/09/13-00:23:00][main][INFO]: output reports_chunk =
reports {
  message: "\032>\010\203\314\257\240%\022 \n\025\010\301\240\360\372\005\020\340\250\001\030\317\377\377\377\377\377\377\377\377\001\022\005ru_RU(\001\032\024\010\004\020\n\030\007:\002\030\001h\001\200\001\252\017\210\001\203\004\032\317\003\010\204\314\257\240%\022 \n\025\010\202\245\361\372\005\020\340\250\001\030\317\377\377\377\377\377\377\377\377\001\022\005ru_RU(\001\032\024\010\000\020\000\030\002:\002\030\001h\001\200\001\253\017\210\001\204\004\032J\010\001\020\000\030\034*4{\"dfid\":{\"battery\":100,\"boot_time_seconds\":3692956}}:\002\030\001h\001\200\001\254\017\210\001\241\005\032\254\002\010\002\020y\030\004\"\010sdk_list*\211\002{\"AppMetrica\":{\"classes\":[\"com.yandex.metrica.YandexMetrica\"]},\"AppMetricaPush\":{\"classes\":[\"com.yandex.metrica.push.YandexMetricaPush\"]},\"Firebase\":{\"classes\":[\"com.google.firebase.messaging.FirebaseMessagingService\",\"com.google.firebase.iid.FirebaseInstanceId\"]}}:\002\030\001h\001x\000\200\001\255\017\210\001\265\001\032\024\010\003\020z\030\007:\002\030\001h\001\200\001\256\017\210\001\204\004\032\211\001\010\205\314\257\240%\022 \n\025\010\243\245\362\372\005\020\340\250\001\030\317\377\377\377\377\377\377\377\377\001\022\005ru_RU(\001\032\024\010\000\020\000\030\002:\002\030\001h\001\200\001\257\017\210\001\205\004\032I\010\001\020\000\030\034*3{\"dfid\":{\"battery\":94,\"boot_time_seconds\":3709373}}:\002\030\001h\001\200\001\260\017\210\001\242\005\"D\n c2bf1010d51d4813a285f808000fbcdb\022 e8e69615b4daf274fa38d5b2c2a03aeeB\033\n\006dummy0\022\02182:C9:BA:02:81:9DB\033\n\006rmnet6\022\02158:02:03:04:05:0CB \n\013rmnet_tun10\022\02158:02:03:04:05:16B\033\n\006rmnet2\022\02158:02:03:04:05:08B\033\n\006rmnet3\022\02158:02:03:04:05:09B\"\n\rrmnet_r_ims10\022\02158:02:03:04:05:10B\033\n\006rmnet4\022\02158:02:03:04:05:0AB\033\n\006rmnet5\022\02158:02:03:04:05:0BB \n\013rmnet_tun14\022\02158:02:03:04:05:1AB\032\n\005wlan0\022\021D8:C7:71:E0:03:7CB \n\013rmnet_tun13\022\02158:02:03:04:05:19B \n\013rmnet_tun12\022\02158:02:03:04:05:18B\033\n\006rmnet0\022\02158:02:03:04:05:06B \n\013rmnet_tun11\022\02158:02:03:04:05:17B\033\n\006rmnet1\022\02158:02:03:04:05:07B \n\013rmnet_ims00\022\02158:02:03:04:05:0DB\"\n\rrmnet_r_ims00\022\02158:02:03:04:05:0EB \n\013rmnet_tun03\022\02158:02:03:04:05:14B \n\013rmnet_tun02\022\02158:02:03:04:05:13B \n\013rmnet_tun01\022\02158:02:03:04:05:12B \n\013rmnet_tun00\022\02158:02:03:04:05:11B \n\013rmnet_ims10\022\02158:02:03:04:05:0FB \n\013rmnet_tun04\022\02158:02:03:04:05:15B\037\n\nrmnet_emc0\022\02158:02:03:04:05:1BR\016\010\372\001\020c\032\007BeelineZ;5D:22:42:74:D9:37:7C:35:DA:77:7A:D9:34:C6:5C:8C:CA:6E:7A:20"
  client_ip: ""
  device_id_hash: 0
  request_parameters {
    uuid: "c2bf1010d51d4813a285f808000fbcdb"
    device_id: "e8e69615b4daf274fa38d5b2c2a03aee"
    app_platform: "android"
    app_version_name: "1.7.2"
    app_id: "ru.yandex.test.pushsample"
    manufacturer: "HUAWEI"
    model: "STF-L09"
    os_version: "9"
    screen_width: 1920
    screen_height: 1080
    screen_dpi: 480
    scale_factor: 3.0
    locale: "ru_RU"
    device_type: PHONE
    is_rooted: false
    app_build_number: 10027
    android_id: "177f9d75cd079c31"
    adv_id: "b9e25b68-087d-49fd-bc44-18ece8efa58f"
    api_key_128: "20799a27-fa80-4b36-b2db-0f8141f24180"
    app_framework: NATIVE
    os_api_level: 28
    kit_build_type: INTERNAL_BINARY
    kit_build_number: 66494
    app_debuggable: false
    limit_ad_tracking: false
    is_request_encrypted: false
    kit_version_name: "3.8.0"
    request_id: 248
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
}
reports {
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
}
```
