Бекенд автобусов
================

Как поднять
-----------
1. скачиваем в корень проекта ресурсы:

   * [TRAVEL_DICT_RASP_STATION_PROD](https://sandbox.yandex-team.ru/resources?type=TRAVEL_DICT_RASP_STATION_PROD)
   * [TRAVEL_DICT_RASP_SETTLEMENT_PROD](https://sandbox.yandex-team.ru/resources?type=TRAVEL_DICT_RASP_SETTLEMENT_PROD)
   * [TRAVEL_DICT_RASP_TIMEZONE_PROD](https://sandbox.yandex-team.ru/resources?type=TRAVEL_DICT_RASP_TIMEZONE_PROD)

   ```shell
   cd $ARCADIA/travel/buses/backend
   wget http://sandbox-storage37.search.yandex.net:13578/resource/1764773280/timezone.data
   ```

1. Получаем [OAuth](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
   токен к секретнице и складываем например сюда ~/.yav/token

1. Запускаем worker
   ```
   cd $ARCADIA/travel/buses/backend/cmd/worker
   ya make .
   TRAVEL_VAULT_OAUTH_TOKEN=`cat ~/.yav/token` CONFIG_PATH=./../../docker/worker/config.development.yaml ./worker
   ```

1. Запускаем api
   ```
   cd $ARCADIA/travel/buses/backend/cmd/api
   ya make .
   TRAVEL_VAULT_OAUTH_TOKEN=`cat ~/.yav/token` CONFIG_PATH=./../../docker/api/config.development.yaml ./api
   ```

Обновить схему логфеллера
---------
```
$a/contrib/tools/protoc/protoc --descriptor_set_out=$a/logfeller/configs/parsers/travel-buses-worker-communication-log.desc -I$a -I$a/contrib/libs/protobuf -I$a/travel/buses/backend/proto -I$a/travel/proto/ -I$a/contrib/libs/googleapis-common-protos -I$a/contrib/libs/protobuf/src --include_imports --include_source_info -I. ./worker_service.proto
```

Запустить в докере
---------
```
cd $ARCADIA/travel/buses/backend
ya package ./pkg.api.json --docker --docker-registry=local --custom-version=local
```

Профилирование
---------
Хендлер профайлера: http://127.0.0.1:9000/debug/pprof/

Для более полного профайлинга нужно собрать с
```
ya make --build profile
```

Mem
```
go tool pprof http://127.0.0.1:9000/debug/pprof/heap?seconds=30
(pprof) web
```

CPU
```
go tool pprof http://127.0.0.1:9000/debug/pprof/profile?seconds=30
(pprof) web
```
