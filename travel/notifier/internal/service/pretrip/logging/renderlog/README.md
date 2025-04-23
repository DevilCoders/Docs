Logfeller
----
- Схема: https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-notifier-pretrip-render-log.desc
- Stream: https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/travel_avia_hahn_streams.json
- Log: https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/travel_avia_hahn_logs.json

Обновить схему в Logfeller
----
```shell
cd $ARCADIA
ya make --yt-store ./contrib/tools/protoc
./contrib/tools/protoc/protoc --descriptor_set_out=./logfeller/configs/parsers/travel-notifier-pretrip-render-log.desc -I ./contrib/libs/protobuf/src/ -I. ./travel/notifier/internal/service/pretrip/logging/renderlog/record/record.proto
```
