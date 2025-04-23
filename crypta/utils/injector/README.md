### Injector
Всовывает кастомные связки в лог rtmr/crypta-to-bigb.  
Пример использования:  
`$ TVM_SECRET="secret" ./injector --link duid:16163252241062278803 --link yandexuid:4077933261494413843`

Вывод:
```
INFO: 2021-03-30 16:54:32.183 +0300 main.cpp:22 Writing to: logbroker.yandex.net/rtmr/crypta-to-bigb by crypta-rtdi-test.
INFO: 2021-03-30 16:54:32.360 +0300 links.cpp:60 Sending: {"Vertices":[{"IdType":37,"Id":"16163252241062278803"},{"IdType":1,"Id":"4077933261494413843"}],"LogSource":1,"LogEventTimestamp":1618482819,"Usage":[1]}
INFO: 2021-03-30 16:54:32.457 +0300 main.cpp:34 Written succesfully.
```
Значения ключей:
* `--link` -- https://a.yandex-team.ru/arc/trunk/arcadia/crypta/lib/proto/identifiers/id_type.proto
* `--log-source` -- https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/proto/log_source.proto
* `--source-type` -- https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/proto/source_type.proto
