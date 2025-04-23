# Piper

## Монотонный рост piper-lb-length

- Проверить, связан ли рост с [входным потоком](https://solomon.yandex-team.ru/?b=2021-07-07T11%3A01%3A29.220Z&e=2021-07-08T11%3A01%3A29.220Z&project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesWritten%2A&TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers&Topic=%21total&Producer=%21total).
- Если входной потом не менялся, то возможно залипла [конкретная партиция](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-qoffers?page=statistics&type=topic&tab=partitions&shownTopics=all%20topics&consumer=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&metricsFrom=1625655755465&metricsTo=1625742155465&sortOrder=%5B%7B%22columnId%22%3A%22readIdle%22%2C%22order%22%3A-1%7D%5D) (отсортировать по "read lag"/"read idle time").
- Зайти на хост, где "read lag"/"read idle time" имеет высокое значение (десятки минут).
- Для безопасного завершения работы piper выполнить (подставить Port):
```
grep '<DaemonConfig>' -A 20 logs/datacamp-piper.log | grep Port | head -n 1
        Port : 18669
curl 'http://localhost:{Port}/?command=restart'
```
- Операция перезапуска небыстрая. Ждать. Если не помогло с лагом, выполнить (опасно, т.к. все, что не успело отправиться в RTY, уже не отправится):
```
pkill -9 piper_new
```


## Разворачиватель топиков

### Предупреждение
Рекомендуется запускать разворачиватель только на одном инстансе, а на остальных выключать чтение проблемного топика.
При OOMах, крэшах пайпера завершение TUnitedStorageUpdater без [DoStop()](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/lib/datacamp_storage_updater/united_updater.h?rev=r8705156#L165) (обновление конфига через its обычно приводит к крэшу пайпера) могут теряться данные размером до 64мб на каждый инстанс, потому что данные отправляются в таблицу происходит по мере накопления определенного размера.

**Внимание!** Если вы разворачиваете топик, который может создавать офферы, необходимо временно добавить ридер собранной таблицы в scanner в [источники](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/scanner/etc/common_processors.cfg?rev=r8876374#L38), которе могут создавать офферы (временно, через its, потом настройку удалить).

### Инструкция по применению
Если piper не успевает вычитать очередь из logbroker, очередь растет, и цены доезжают до хранилища с опозданием. Решить эту проблему призван "разворачиватель топиков". Он снимает очередь с piper и передает ее scaner. Для решения проблем в проде предлагается использовать **только один** из инстансов prastable.
Вот как это происходит:
- Для начала необходимо выключить чтение проблемного топика во всех контейнерах через its, чтобы партиции топика не были заняты другими инстансами.
```
{
  "env_conf": [
    {
      "values": {
        "UNITED_MINER_INPUT_ENABLED": "false"
      }
    }
  ]
}
```
- Далее на одном единственном prestable контейнере изменить конфигурацию piper следующим образом:
```
{
  "env_conf": [
    {
      "values": {
        "UNITED_MINER_INPUT_ENABLED": "true",
        "PIPER_QUEUE_DUMP_TABLE": "//home/market/production/indexer/datacamp/united/tmp/piper_queue_dump",
        "UNITED_UPDATER_PIPER_QUEUE_DUMP_SOURCES": "MinerUnpacker"
      }
    }
  ]
}
```
Если указана переменная среды UNITED_UPDATER_PIPER_QUEUE_DUMP_SOURCES, то нужно обязательно указать PIPER_QUEUE_DUMP_TABLE, [иначе пайпер не запустится](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/lib/datacamp_storage_updater/config.cpp?rev=r8710602#L62).
Можно так же регулировать количество процессоров в пуле асинхронной записи в таблицу `"Proxy.Processors.UnitedOffersUpdater.PiperQueueDumpThreads": "5"` и частоту пересоздания писателя `"Proxy.Processors.UnitedOffersUpdater.PiperQueueDumpOffersLimitPerWriter": 100000`

- Контролировать процесс дампа можно по графикам:
   * [Лаг чтения сообщений из топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-from-miner&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=MessageLagByLastRead&graph=auto&checks=&b=2021-10-01T07%3A44%3A07.593Z&e=2021-09-30T18%3A16%3A15.017Z)

   * [График офферов, распакованных из сообщений логброкера, и график офферов, отправленных в статическую таблицу.](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;ctype=production;signals=%7Bunistat-MinerUnpacker_offers_processed_dmmm,unistat-UnitedOffersUpdater_offers_dumped_counter_dmmm%7D/?from=1633071000000&to=1633072500000)

   * [Количество обработанных батчей и сообщений - график 3хх, количество ошибок - график 5хх](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;ctype=production;signals=%7Bunistat-UnitedMinerMulticlusterInput_reply_3xx_dmmm,unistat-UnitedMinerMulticlusterInput_reply_5xx_dmmm%7D/?from=1633071000000&to=1633072500000)

   * [График времени дампа одного батча целиком, и график времени создания писателя в ыть](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;ctype=production;signals=%7Bquant(unistat-UnitedOffersUpdater_tx_batch_dump_ms_dhhh,99),quant(unistat-UnitedOffersUpdater_writer_created_ms_dhhh,99)%7D/?from=1633071000000&to=1633072500000) (включает в себя время создания писателя).

- Вернуть конфиги на всех инстансах назад в исходное состояние. Теперь piper будет читать свежие данные из топика.

- Отсортировать данные в таблице по [ключу из таблицы](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/tables/PiperQueueDumpSchema.proto?rev=r8585187#L7)
```
yt sort --proxy=arnold \
    --src //home/market/production/indexer/datacamp/united/tmp/piper_queue_dump \
    --dst //home/market/production/indexer/datacamp/united/tmp/piper_queue_dump_sorted \
    --sort-by business_id --sort-by shop_sku
```

- Добавить через its в конфигурацию scanner
```
{
  "env_conf": [
    {
      "values": {
        "PIPER_QUEUE_DUMP_TABLE": "//home/market/production/indexer/datacamp/united/tmp/piper_queue_dump_sorted"
      }
    }
  ]
}
```
Можно так же регулировать `"Proxy.Processors.YtPiperQueueDumpTableReader.MaxInflight": "5"`

- Временные таблицы могут потреблять большое количество чанков из нашей квоты в YT, поэтому после устранения очереди в лоброкере рекомендуется удалить временные таблицы
```
yt remove --proxy=arnold --path //home/market/production/indexer/datacamp/united/tmp/piper_queue_dump
yt remove --proxy=arnold --path //home/market/production/indexer/datacamp/united/tmp/piper_queue_dump_sorted
```

В результате piper будет доставлять свежие обновления в хранилище, а очередью займется scanner.
Маркет спасен, а вы - молодец!
