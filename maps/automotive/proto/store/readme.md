## Automotive external store API

## To get protobuf versions of examples:
cat examples/app_details | protoc --encode=yandex.automotive.proto.store.AppDetails -I. -I../../../doc/proto store.proto > examples/app_details.pb
cat examples/app_list | protoc --encode=yandex.automotive.proto.store.AppListResponse -I. -I../../../doc/proto store.proto > examples/app_list.pb
cat examples/download_meta | protoc --encode=yandex.automotive.proto.store.DownloadMeta -I. -I../../../doc/proto store.proto > examples/download_meta.pb

## API description
https://wiki.yandex-team.ru/elenamarkova/auto/3rdpartyapps/api/
