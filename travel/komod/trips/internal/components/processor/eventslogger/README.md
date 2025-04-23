### Лог событий процессинга заказов для генерации поездок пользователей

#### Топики в logbroker
- [testing](https://lb.yandex-team.ru/logbroker/accounts/avia/testing/trips/processing-event-log)
- [production](https://lb.yandex-team.ru/logbroker/accounts/avia/production/trips/processing-event-log)

#### Обновить .desc файл в logfeller
```shell
cd $ARCADIA/contrib/tools/protoc/bin
ya make .
cd $ARCADIA
./contrib/tools/protoc/bin/protoc \
  --descriptor_set_out=./logfeller/configs/parsers/travel-trips-processing-events-log.desc \
  --include_imports \
  --include_source_info \
  -I ./contrib/libs/protobuf/src/ \
  -I. ./travel/komod/trips/internal/components/processor/eventslogger/proto/record.proto
```
