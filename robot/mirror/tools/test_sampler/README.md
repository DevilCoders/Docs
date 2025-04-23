# test_sampler

Эта утилитка читает данные с LogBroker'а и записывает их в QYT.

## Как задать конфиг

Конфиг лежит в /arcadia/robot/mirror/config/test_sampler

Для начала необходимо создать bit_rt очередь и consumer'а для нее. Сделать это можно с помощью /arcadia/ads/bsyeti/big_rt/cli/big_rt_cli. Заменить под себя поля:
* YtCluster
* YtPath
* Consumer:MainPath
* Consumer:Cluster

Далее у всех Supplier'ов необходимо поменять поля "LogbrokerClientId и "SrcTopic" на свои значения.

Пример запуска утилитки:
 ```console
TVM_TOKEN="<Ваш TVM_TOKEN>" TVM_ID=<Ваш TVM_ID> ./test_sampler --config-file config.json
```