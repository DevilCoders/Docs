# Clickdaemon protobuf API

With each change to these files you should regenerate logfeller proto descriptors by running this command:

```sh
$ARCADIA/contrib/tools/protoc/protoc --descriptor_set_out $ARCADIA/logfeller/configs/parsers/quasar-device-proto-metrics.desc --proto_path $ARCADIA --proto_path $ARCADIA/contrib/libs/protobuf/ --include_imports --include_source_info -I. $ARCADIA/infra/proto_logger/api/api.proto
```
