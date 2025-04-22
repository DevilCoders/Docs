# Изменение модели

## Перегенерация парсера для logfeller
События, отправленные в логброкер, дальше раскладываются в yt таблицы с помощью логфеллера. Для этого в конфиге 
логфеллера есть парсер, который необходимо обновлять при изменении модели. Последовательность следущая:
1. Собрать protoc - выполнить ya make в arcadia/contrib/tools/protoc/bin
2. Выполнить команду в директории с logistic_event.proto
```
~/arc/arcadia/contrib/tools/protoc/bin/protoc --descriptor_set_out ~/arc/arcadia/logfeller/configs/parsers/market-l4s-logistic-events-log.desc --proto_path ~/arc/arcadia --proto_path ~/arc/arcadia/contrib/libs/protobuf/src --proto_path ~/arc/arcadia/contrib/libs/googleapis-common-protos --include_imports --include_source_info -I. logistic_event.proto
```
3. Запушить новую версию парсера market-l4s-logistic-events-log.desc в транк 

## Как проверить парсер
Можно проверить парсер локально, для этого нужно:
1. ya make в arcadia/logfeller/bin/stdin_parser
2. ```
   cat <raw_bytes_file> | ./logfeller-stdin-parser --parser market-l4s-logistic-events-log --configs ~/arc/arcadia/logfeller/configs/parsers
   ```
