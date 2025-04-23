# Комбинатор (combinator)

## Полезные ссылки
1. [wiki: Combinator](https://wiki.yandex-team.ru/market/development/purple/combinator)
2. [wiki: Delivery Combinator техкарточка](https://wiki.yandex-team.ru/users/kanaglic/delivery-combinator/)
3. [wiki: Описание устройства тариффов](https://wiki.yandex-team.ru/delivery/development/flattariff/documentatiofforsd/)
4. [Пример тарифа в xml](https://paste.yandex-team.ru/937859)
5. [Код php](https://github.yandex-team.ru/delivery/delivery/blob/cb86e7614ede58ecc601c64d39462634ef567217/common/components/YaMarket/Integration/Exporter/Tariff/Writer.php)

## Проектное
1. [abc](https://abc.yandex-team.ru/services/combinator/)
1. [robot-combinator](https://staff.yandex-team.ru/robot-combinator)
1. [startrek](https://st.yandex-team.ru/combinator)

## Компонент tariff2yt
[cmd](https://a.yandex-team.ru/arc/trunk/arcadia/market/combinator/cmd/tariff2yt/README.md)
Для записи в YT использует индексаторные токены, отдельные для тестинга и прода.

## RTC nanny
### tariff2yt
1. [testing_market_tariff2yt_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_tariff2yt_vla/)
1. [production_market_tariff2yt_man](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tariff2yt_man/)
1. [production_market_tariff2yt_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tariff2yt_sas/)
1. [production_market_tariff2yt_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tariff2yt_vla/)

### combinator
1. [testing_market_combinator_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_combinator_sas/)
1. [testing_market_combinator_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_combinator_vla/)
1. [production_market_combinator_man](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_combinator_man/)
1. [production_market_combinator_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_combinator_sas/)
1. [production_market_combinator_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_combinator_vla/)

### ITS
1. [its combinator](https://nanny.yandex-team.ru/ui/#/its/locations/market/combinator/)

## TSUM релизы
1. [tsum tariff2yt](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/tariff2yt)
2. [tsum combinator](https://tsum.yandex-team.ru/pipe/projects/report/delivery-dashboard/combinator)

## YT данные
### tariff2yt создает, combinator читает
1. [test_hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/indexer/combinator)
1. [test_arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/combinator)
1. [prod_hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/combinator)
1. [prod_arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/combinator)
### Исходные данные для графа (PostgreSQL => Transfer Manager => dynamic tables)
1. [test_hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/cdc/test/market/logistics_management_service/combinator&)
1. [prod_hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/cdc/prod/market/logistics_management_service/combinator&)
1. [prod_arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/cdc/prod/market/logistics_management_service/combinator&)

## Приборы
1. [Комбинатор grafana](https://grafana.yandex-team.ru/d/0LtqIGZGk/combinator?orgId=1)
2. [Комбинатор graphite](https://market-graphite.yandex-team.ru/dashboard#combinator)
3. [Комбинатор Solomon, есть выбор ручки](https://solomon.yandex-team.ru/?project=market-combinator&dashboard=combinator_courier_sku_offers)

### Dev
1. [grpc log parser](https://github.yandex-team.ru/market-infra/market-health/blob/master/logshatter/src/main/java/ru/yandex/market/logshatter/parser/marketout/CombinatorLogParser.java)
1. [logshatter config](https://github.yandex-team.ru/market-infra/market-health/blob/master/config-cs-logshatter/src/conf.d/combinator_grpc.json)
1. [clickphite config](https://github.yandex-team.ru/market-infra/market-health/blob/master/config-cs-clickphite/src/conf.d/combinator_grpc.json)

## API
### Ручки testing
1. http://combinator.tst.vs.market.yandex.net/ping
2. http://combinator.tst.vs.market.yandex.net/status

```sh
manushkin@laptop:~$ curl -s http://combinator.tst.vs.market.yandex.net/status| jq .
{
  "SvnRevision": "6850154",
  "SvnDate": "2020-05-20T21:32:51.000000Z",
  "StartTime": "2020-05-21T00:39:49.845036118+03:00",
  "Hostname": "vla1-5925-vla-market-test-comb-31c-19119.gencfg-c.yandex.net",
  "IsOpen": true,
  "Meta": {
    "Name": "20200521_104410",
    "DirPath": "//home/market/testing/indexer/combinator/generation/20200521_104410",
    "Generations": {
      "geobase": "//home/market/testing/indexer/combinator/geobase/20200519_090048",
      "graph": "//home/market/testing/indexer/combinator/graph/20200520_130428",
      "tariffs": "//home/market/testing/indexer/combinator/tariffs/20200521_104303"
    }
  }
}
```

### Ручки production
1. http://combinator.vs.market.yandex.net/ping
2. http://combinator.vs.market.yandex.net/status

### GRPC
Балансер слушает http/2 на порту 8080.
```
manushkin@public01v:~$ grpcurl -plaintext combinator.tst.vs.market.yandex.net:8080 list
Market.PingService
grpc.reflection.v1alpha.ServerReflection
yandex.market.combinator.v0.Combinator

manushkin@public01v:~$ grpcurl -plaintext combinator.tst.vs.market.yandex.net:8080 list Market.PingService
Market.PingService.ping

manushkin@public01v:~$ grpcurl -plaintext combinator.tst.vs.market.yandex.net:8080 describe Market.PingService
Market.PingService is a service:
service PingService {
  rpc ping ( .google.protobuf.Empty ) returns ( .Market.PingResponse );
}

manushkin@public01v:~$ grpcurl -plaintext combinator.tst.vs.market.yandex.net:8080 Market.PingService/ping
{
  "state": true,
  "message": "0;ok"
}
```

#### grpcurl
https://github.com/fullstorydev/grpcurl

## CLI (Command Line Interface)
### grpc_client
```
manushkin@laptop:~/src/arcadia/market/combinator$ ya make -r && cmd/grpc_client/combgrpc
/home/manushkin/src/arcadia/ya make -r
Ok
Usage:
  combgrpc [command]

Available Commands:
  delivery-options     Make GetDeliveryOptions request
  delivery-route       Make GetDeliveryRoute request
  help                 Help about any command
  offer-delivery-stats Make GetOffersDeliveryStats request
  pickup-points        Make GetPickupPoints request

Flags:
      --address string      Address of combinator server (default "combinator.tst.vs.market.yandex.net:8080")
      --file string         Path to file where to save response
  -h, --help                help for combgrpc
      --max-resp-size int   Maximal response size (default 10000000)

Use "combgrpc [command] --help" for more information about a command.
```
Пример запуска команды `offer-delivery-stats`: https://paste.yandex-team.ru/1066257


## Устройство (dev)
При добавлении новых разделов советуется посмотреть примеры хороших практик для расположения кода в GO проектах.
[Пример устройства проекта на GO](https://github.com/golang-standards/project-layout)

### CMD
*Директория, в которой хранятся исполняемы файлы (package main)*

В эту директорию стоит складывать небольшие файлы, которые будут запускать код, описанный в пакетах из [pkg](#PKG)

### PKG
*Директория, в которой хранятся новые самописные пакеты*

В эту директорию помещается всё, что касается библиотечного кода.

### DEPLOY
*Директория, в которой хранятся описания пакетов для деплоя (pkg.json)*

В эту директорию помещается json описания пакета, а также основной бинарник для его запуска.

# Разработка

## combinator-app

1. Сборка и запуск с чтением данных из YT:
   ```bash
   ./run_app
   ```

2. Сборка и запуск с чтением данных с локальной фаловой системы:
   ```bash
   ./prepare_data.py pdata
   ./run_app -local-dir pdata/
   ```

3. Для того, чтобы логика расчета совпадала с продовой, необходимо подложить its-файлик
 - скачать его можно тут [its combinator](https://nanny.yandex-team.ru/ui/#/its/locations/market/combinator/)
 - положить в `root/controls/its_market_combinator.json` относительно папки запуска (combinator)

## Профилирование

1. скачиваем данные:
   ```bash
   ./prepare_data.py
   ```

2. запускаем программу:
   ```bash
   ./timeit
   ```

3. запускаем профайлер:
   ```bash
   ya tool go tool pprof ./profile.cpu
   ```

Примеры команд для профайлера:
1. ```(pprof) top 33```
2. ```(pprof) top 33 -cum```
3. ```(pprof) list routes.*GetOffersDeliveryStats$```

## Отладка

#### Подготовка:
1. `ya tool go get -u github.com/go-delve/delve/cmd/dlv` установить один раз отладчик.
2. Проверить, что бинарники из `GOPATH` доступны (`export PATH=$PATH:$GOPATH/bin` в `.bashrc` или `.zshrc`)
3. (для goland) Импортировать себе `combinator-local.run.xml` (положить в `.idea/runConfigurations/combinator_local.xml`)

#### Запуск:

1. ```bash
    ./prepare_data.py #опциональная подготовка локальных данных
    ./run_debugger -local-dir pdata #передача флагов в приложение
   ```

2. Goland: Run->Debug Combinator local

3. Остановить: в соседней(!) консоле `./stop_debugger`

