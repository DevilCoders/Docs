# Content-storage

Микросервис на шайни, в первую очередь используется для быстрой доставки данных контентов клиентам

### Подробнее можно почитать тут:
https://wiki.yandex-team.ru/users/ya-spe/modelinfo/implementation/

https://wiki.yandex-team.ru/users/d-burkov/content-storage-dezhurstvo/

### Текущие ручки:

**/card_info** (http + grpc) - получение данных о карточках.

Формат запроса/ответа: https://a.yandex-team.ru/arc/trunk/arcadia/market/content_storage_service/proto/card_info.proto?#L6

Пример:
```bash
curl -X GET http://market-content-storage.tst.vs.market.yandex.net:80/card_info --data '{"market_skus": [100439187565], "model_ids": [217320405]}'
```

**/render_gumoful** (http + grpc) - возвращает отрендеренные шаблоны карточек.

Формат запроса/ответа: https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/cs/CsGumofulService.proto?#L23

Пример:
```bash
curl -X GET http://market-content-storage.tst.vs.market.yandex.net:80/card_info --data <данные в формате: https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/cs/CsGumofulService.proto?#L22>
```

**/experiments** (http) - получить текущие дефолтные значения экспериментов.

**/versions** (http) - получить версии данных.


### Чтобы попробовать:
1) Выкачать к себе данные актуальных ресурсов MARKET_CS_DATA_PROD, MARKET_CS_PERS_DATA_PROD и MARKET_CS_RECOM_DATA
2) Указать путь до них в конфиге: https://a.yandex-team.ru/arc/trunk/arcadia/market/content_storage_service/bin/cfg.local?#L27
3) Если хотим походить в прод/тестинг, то крадем SaasConfig и ReportConfig из соответствующих конфигов
4) Чтобы заработал клиент для сааса, ему необходим правильных tvm токен, их можно взять в abc-шнице. Значение секрета нужно положить в переменную окружения TVM_SECRET
5) Теперь можно запускать cs под gdb:
```bash
ya tool gdb --args ./bin -c cfg.local -p <port>  (из content_storage_service/bin)
```

![](https://avatars.mds.yandex.net/get-zen_doc/1583807/pub_5e1755a73639e600b0d13cad_5e175a18ba281e00b0bf2b29/scale_1200)
