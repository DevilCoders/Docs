## Конвертация всех докуменов из хранилища для отправки в SaaS

В случае когда срочно требуется обновить весь стейт документов в SaaS
```
./saas_docs_dumper --help
Usage: ./v [OPTIONS] [ARG]...

Options:
  {-V|--svnrevision}  print svn version
  {-?|--help}         print usage
  --yt-proxy VAL
  --yt-token-path VAL
  --yt-pool VAL
  --basic-table VAL
  --service-table VAL
  --identifiers-white-list-table VAL
  --business-id VAL
  --output-table VAL

Free args: min: 0, max: unlimited
```

1. Запускаем бинарник с таблицами ЕОХ, опционально можно построить таблицу для определенных business_id с помощью параметра `--business-id`, либо передать таблицу с идентификаторами офферов с помощью параметра `--identifiers-white-list-table`
2. Итоговую таблицу можно провалидировать на глаз с помощью тулзы [map_to_readable](https://a.yandex-team.ru/arc/trunk/arcadia/saas/tools/map_to_readable)

### Отправка документов с помощью saas_push, предпочитительный вариант 
У команды SaaS есть тулза для отправки сообщений в топик logbroker https://wiki.yandex-team.ru/jandekspoisk/saas/DataDelivery/PQ/Demon-dlja-zapisi-v-SaaS-cherez-LB/#zalivkaiztablicynayt. Тулза очень медленная, где-то 500 офферов в минуту, основной затуп происходит при записи в топик. 

Конфиг для saas_push, дополнительно необходимо задать TVM_SECRET хранилища:
```
<Controller>
    <HttpOptions>
        Port : 19025
        Threads : 1
    </HttpOptions>
</Controller>
<Telemetry>
    Interval: 10m
</Telemetry>
<Server>
    Log : logs/global.log
    TvmLog : logs/tvm.log
    LogbrokerLog : logs/lb.log
    <PQLibSettings>
        ThreadsCount: 1
        CompressionPoolThreads: 1
        GRpcThreads: 1
    </PQLibSettings>
    <SearchMap>
        Ctype : stable_market_idx
        DMHost : saas-dm-proxy.n.yandex-team.ru
        StaticaHost : saas-searchmap.s3.mds.yandex.net
        StaticaQuery : stable_market_idx
    </SearchMap>
    <Writer>
        <HttpOptions>
            Port : 19024
            Threads : 1
        </HttpOptions>
        MessagesLog: logs/message.log
        <Service>
            Alias: market-datacamp-stable
            Name: market_datacamp
            Ctype: stable_market_idx
            Server: logbroker.yandex.net
            TopicsDir: /saas/services/market_datacamp/stable/topics
            Format: Proto
            <TVM>
                DestinationAlias: logbroker
                DestinationClientId: 2001059
                ClientId: 2016907
            </TVM>
            LoggingEnabled: true
            <CheckMessage>
                Disabled: true
            </CheckMessage>
        </Service>
        <Service>
            Alias: market-datacamp-prestable
            Name: market_datacamp
            Ctype: prestable_market_idx
            Server: logbroker.yandex.net
            TopicsDir: /saas/services/market_datacamp/prestable_market_idx/topics
            Format: Proto
            <TVM>
                DestinationAlias: logbroker
                DestinationClientId: 2001059
                ClientId: 2002296
            </TVM>
            LoggingEnabled: true
            <CheckMessage>
                Disabled: true
            </CheckMessage>
        </Service>
    </Writer>
</Server>
```

### Отправка документов с помощью ферримана
!!! ИСПОЛЬЗОВАТЬ ТОЛЬКО ВО ВРЕМЯ ФАКАПИЩА, ТАК КАК СОТРЕТ ВСЕ БЕКАПЫ В SAAS, потом придется все переналивать через logbroker. И заранее согласовать с командой saas.

1. Отправляем в ферриман таблицу для варки индекса
```bash
TABLE_PATH={};YT_PROXY={}; curl "market-datacamp.ferryman.n.yandex-team.ru/add-table?path=$TABLE_PATH&namespace=0&timestamp=$(date +%s)000000&delta=false&cluster=$YT_PROXY"
   {"batch":"1616152303559437"}`
```
2. Следим за статусом варки индекса
```bash
BATCH_ID={}; curl "http://market-datacamp.ferryman.n.yandex-team.ru/get-batch-status?batch=$BATCH_ID"
{"status":"queue"}
BATCH_ID={}; curl "http://market-datacamp.ferryman.n.yandex-team.ru/get-batch-status?batch=$BATCH_ID"
{"status":"final"}
```

### Почитать
* [Про ferryman](https://wiki.yandex-team.ru/jandekspoisk/SaaS/Ferryman/)
