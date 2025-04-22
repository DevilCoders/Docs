## Администрирование

```
Прод - https://datacamp-admin.white.vs.market.yandex.net
Тестинг - https://datacamp-admin.white.tst.vs.market.yandex.net
```

### Swagger:
```
Прод - https://datacamp-admin.white.vs.market.yandex.net/docs/#/
Тестинг - https://datacamp-admin.white.tst.vs.market.yandex.net/docs/#/
```

### POST /mine
Отправить данные на обогащение по набору business_id
```
$ curl -XPOST https://datacamp-admin.white.vs.market.yandex.net/mine?business_id=<business_id_1>&business_id=<business_id_2>
Start mine at 1631283194 for businesses: business_id_1,business_id_2
```

Альтернативный способ передачи идентификаторов бизнесов:
```
$ curl -XPOST -H "Content-Type: application/json" https://datacamp-admin.white.vs.market.yandex.net/mine -d '{"businesses": [1, 2]}'
Start mine at 1631283194 for businesses: 1, 2
```

Есть возможность указать дополнительные параметры:
- lower_ts - будут майниться только офферы, майнившиеся после этой отметки времени (UTC в секундах)
- upper_ts - будут майниться только офферы, майнившиеся до этой отметки времени (UTC в секундах)
- verdict_code - будут майниться только офферы с вердиктом (resolution.by_source), внутри которого заданный код

В случае, если какая-то часть офферов не помайнилась, рекомендуется указывать в upper_ts значение, которое вернулось в предыдущем ответе ручки. В таком случае то, что уже помайнилось по нашей инициативе, не будет отправленно на майнинг еще раз.

Чтобы определить бизнесы, которые нужно отправить на майнинг, можно использовать [yql-скрипт](https://yql.yandex-team.ru/Operations/YT88n5fFtwh1pqiN0Ai7wLlQbiLh9AgRxqqp5c5TnDU=). Далее, для майнинга, качаем файл полного результата (View full result) в формате tsv, преобразуем его в json формат, проверяем формат и отправляем на майнинг:
```
$ sed -z 's/\n/,/g' yt___tmp_yql_evlyubimov_60d88579_b6ded32e_1ddcd22a_4c4e056c | sed 's/.$/]}/' | sed 's/business_id,/{"businesses": [/' > businesses
$ jq . businesses | less
$ curl -XPOST -H "Content-Type: application/json" https://datacamp-admin.white.vs.market.yandex.net/mine --data-binary '@businesses'
```

Еще вариант скрипта: для отбора бизнесов с офферами, на которых установлен вердикт с заданным кодом - [yql-скрипт](https://yql.yandex-team.ru/Operations/YaYGxgVK8Klu00kFGd4GwZIyZmhvZlWKWYFDMSKVlKI=).

### POST /mine?sync
Безусловная отправка данных на обогащение по business_id в синхронном режиме, без проверки магазина по таблице partners.
Полезна для случаев, если магазин в таблице partners отсутствует или выключен.

```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/mine?business_id=<business_id_1>&business_id=<business_id_2>&sync"
```

Есть возможность указать дополнительные параметры:
- mining_batch_size - минимальный размер батчей, отправляемых на майнинг (реальный размер зависит от количества клонов)
- ids_table - путь к таблице с идентификаторами офферов для отправки, таблица должна быть отсортирована
- yt_cluster - кластер, на котором хранится таблица
- num_shards - число шардов, которые будут отправляться параллельно, по умолчанию - один шард. Максимальное значение - 40.

Формат таблицы (таблицу надо отсортировать по business_id, shop_sku):
[пример подготовки таблицы](https://yql.yandex-team.ru/Operations/Ye-sjQVK8KlC1PwDXXgjkv6zs60WxELjzxINI2Gn0Sk=)

Пример запуска майнинга по таблице идентификаторов:
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/mine?num_shards=40&yt_cluster=arnold&ids_table=//tmp/yql/evlyubimov/4f99ce43-313f3ba5-9cdc8c97-6726f256"
```

### POST /mine?full
Отправить данные на обогащение все сразу
```
$ curl -XPOST https://datacamp-admin.white.vs.market.yandex.net/mine?full
Start mine at 1631283194 for businesses: 737203,...
```

Далее можно следить за тем, сколько еще магазинов ждут своей очереди force отправки:
```
$ curl https://datacamp-admin.white.vs.market.yandex.net/monitoring?check=check_force_count_miner_state
$ 0;There are 1 businesses with "force=True", they should be touched soon: set([10369797L])
```

Кроме этого можно посмотреть на статус майнинга в таблице [mining_state](https://yql.yandex-team.ru/Operations/YTtpTRJKfWzqRrjdMMZ9rXIrurwTJ8z8h0b4bRUotig=). Для этого надо указать бизнесы, которые вас интересуют, во вложенный файл скрипта.

Если горит мониторинг [mining-queue-length](https://juggler.yandex-team.ru/check_details/?host=mi-datacamp-united&service=mining-queue-length&query=&last=1DAY), то принудительный майнинг пропускается, и выполняется майнинг только по TTL. Принудительный майнинг ждет своей очереди.
Можно следить за отправкой на майниг по [графикам в solomon](https://solomon.yandex-team.ru/?project=market-indexer&dashboard=mined_shops_count).

Для анализа успешности завершения процесса майнига используем yql-скрипты:
- [завершение майнинга сервисных частей определенного набора бизнесов](https://yql.yandex-team.ru/Operations/YT9C7NjKS5vGHivz__FJ7_OgsAtSRj0uzchp_s4fD78=)
- [завершение майнинга всех бизнесов активных магазинов](https://yql.yandex-team.ru/Operations/YT9D9gVK8HLJWzkkw1NKX983vonH-bHNUNlN-jFugfE=)

### POST /make_offers_force_mine_table
Ручка для создания таблицы на перемайнинг, которая потом может использоваться в ручке /mine?sync
Входные параметры:
- input_table: путь к таблице с сервисными офферами, по умолчанию берется из конфига
- output_table: путь к выходной таблице
- from_ts: таймстемп в секундах: оффера с какого времени записать в таблицу
- to_ts: таймстемп в секундах: оффера до какого времени записать в таблицу
- from_version: оффера с версией манера больше этой запишутся в таблицу
- to_version: оффера с версией манера меньше этой запишутся в таблицу
- sort: Сортировать выходную таблицу
- sandbox: запускать в сэндбоксе, по умолчанию true

Ответ:
- запуск локально: `Completed with return code=<error code>`
- запуск в сэндбоксе: `Task started: https://sandbox.yandex-team.ru/task/<task id>/view`
Пример запуска:
```
$ curl -XPOST 'https://datacamp-admin.white.tst.vs.market.yandex.net/make_offers_force_mine_table?output_table=//home/market/testing/indexer/datacamp/tmp/tomine&from_ts=1647232256&sort=true'
```

### PUT /rollback_to_backup
Откат на бэкапную оферную таблицу
    generation - номер поколения таблицы
    reason - причина отката
```
$ curl -XPUT "https://datacamp-admin.white.vs.market.yandex.net/rollback_to_backup?generation=20190905_1811&reason=problem"
{
  "Start rollback to backup 20190905_1811"
}
```
Так как откат на бэкап - длительная операция, ручка возвращает ответ до того, как выполнение отката завершилось. Поэтому получение валидного ответа от ручки не является подтверждением успешного выполнения отката, необходимо следить за логами!!!

### GET /monitoring?check=\<check\>
Возвращает результат проверки (мониторинга)
```
$ curl https://datacamp-admin.white.vs.market.yandex.net/monitoring?check=check_force_count_miner_state
$ 0;There are no shops with "force=True"
```
### POST /send_partners_stock
Отправка партнерских стоков (dropship & crossdock) в топик datacamp-partner-stock
- Все стоки
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_partners_stock"
```
- Конкретные магазины
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_partners_stock?shop_id=<shop_id>&shop_id=<shop_id>"
```
- Конкретные склады
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_partners_stock?warehouse_id=<warehouse_id>&warehouse_id=<warehouse_id>"
```
- По времени (свежее timestamp в секундах)
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_partners_stock?timestamp=<timestamp>"
```
### POST /clean
Запуск очистки таблиц хранилища

1. Очистка данных магазинов. Удаляет из таблиц хранилища записи, удовлетворяющие фильтрам. В этом режиме ручка защищена TVM ([подробности](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#tvm)).
Важно: ручка удаляет только сервисные офферы, базовые остаются нетронутыми и удалятся автоматически рутиной datacamp_cleaner по причине отсутствия связанного сервисного оффера в течение ~2х недель.
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/clean?shop={business_id}-{shop_id}&shop={business_id}-{shop_id}"
```

Дополнительные параметры:
- proxy - yt proxy
- only_disabled (default - 0) - помечаем удаленными только офферы, скрытые партнером
- erase (default - 0) - прямое удаление офферов из таблиц хранилища (без отправки подписчикам)

2. Очистка мусорных данных и данных помеченных как удаленные. Если erase == False и remove == False, то происходит построение таблиц с мусорными офферами, самого удаления не происходит.
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/clean?proxy={yt_proxy}&erase={bool}"
```

3. Запуск удаления набора офферов по таблице. Удаляет офферы по идентификаторам из таблицы. В этом режиме ручка защищена TVM.
Важно: офферы помечаются удаленными и отправляются подписчикам. Окончательное удаление происходит во время прохода клинера. Для удаления офферов без простановки признака удаления и отправки подписчикам есть утилита [delete_offers](https://a.yandex-team.ru/arcadia/market/idx/datacamp/dev/delete_offers/README.md?blame=true&rev=r9522424#L1).
В зависимости от формата таблицы, удаляется либо весь united-оффер, либо его сервисные части.
- для удаления united-офферов используется формат: business_id, offer_id
- для удаления сервисных офферов используется формат: business_id, offer_id, shop_id
```
$ curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/clean?proxy={yt_proxy}&ids_table={table_path}
```

Дополнительные параметры:
- proxy - yt proxy
- ids_table - путь к таблице с идентификаторами офферов для отправки, таблица должна быть отсортирована

### POST /send_to_subscriber
Отправка данных подписчикам
- Целиком бизнес или магазин
- Выборочно оффера с идентификаторами, заданными в таблице

Параметры:
- business_id - бизнес
- shop_id - услуга (сервис)
- table_path - путь до сортированной таблицы в YT с идентификаторами офферов в формате <business_id, offer_id>
- proxy - кластер, на котором лежит таблица
- sync - ожидать завершения отправки (true by default)
- subscriber - подписчик из [списка](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/lib/blueprints/send_to_subscriber.py?rev=r8962822#L14)

Примеры:
```
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/send_to_subscriber?business_id=11027612&subscriber=MBOC_SUBSCRIBER"
```
[Подготавливаем таблицу](https://yql.yandex-team.ru/Operations/YcIH265OD8ePoLyaNrn2ZD3i2TxYdWS8ugdsdpeVvS4=)
```
curl -X POST "https://datacamp-admin.white.vs.market.yandex.net/send_to_subscriber?subscriber=PICROBOT_SUBSCRIBER&proxy=arnold&table_path=//tmp/yql/ana-samokhina/send_pictures"
```


### POST /send_msku
Отправка данных по msku в IRIS
Параметры:
- msku_id - идентификатор msku, который надо отправить, repeated параметр
- yt-table-path - путь до таблицы, если идентификаторы указаны в YT. В таблице должен быть столбец `msku_id` с типом `int64`
- yt-proxy - прокси, где находится таблица

Также можно передать список идентификаторов через в теле запроса, формат есть в примерах.

```bash
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/send_msku?msku_id=123
```

```bash
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/send_msku?yt-table-path=//tmp/isabirzyanov/send_mskus&yt-proxy=arnold
```

```bash
curl -XPOST -H "Content-Type: application/json" https://datacamp-admin.white.tst.vs.market.yandex.net/send_msku -d '{"msku_ids": [1, 2]}'
```

### POST /dump
Генерация свежих таблиц выгрузки датакемпа white_out, blue_out и turbo_out. Индексатор регулярно дергает [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/marketindexer/marketindexer/biggeneration.py?rev=8230900#L1084).

Параметры:
- cluster - кластер
- color - список для генерации, по умолчанию используется ['white', 'blue', 'turbo']

Пример:
```
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/dump?cluster=arnold&color=white&color=blue"
```

### POST /prepare_publication_status_diff
Генерация таблиц различия статусов в хранилище и поколении [publication_status_diff](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/in/publication_status_diff). Индексатор регулярно дергает после сборки поколения [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/marketindexer/marketindexer/build_mass_index.py?rev=r8444198#L1621).

Параметры:
- cluster - кластер
- table - полный путь входной таблицы статусов, пример: //home/market/production/indexer/gibson/out/offers_status/20210722_0221
- datacampdir - (опционально) путь до таблиц с офферами, которые мы пытались взять в поколение, пример: //home/market/production/indexer/stratocaster/mi3/datacamp/20210726_0217
- offer_version_dir - версии офферов из поколения, пример: //home/market/production/indexer/gibson/mi3/offer_version/20210722_0221
- colors - white,blue
- timestamp - пример: 1626915694. С его помощью получается имя результирующей таблицы //home/market/production/indexer/datacamp/united/in/publication_status_diff/20210722_0101

Пример:
```
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/prepare_publication_status_diff?cluster=arnold&color=white,blue"
```

### POST /set_otrace_flag
Установка/снятие trace-флага для офферов. Фактически редирект на [ручку в Stroller'е](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#ustanovkasnyatie-trace-flaga) для обхода TVM.

#### Параметры
Имя | Тип
:--- | :---
business_id | uint, required
shop_id | uint, required
offer_id | list\<string\>, required
unset | flag, optional

Примеры запросов:
```
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/set_otrace_flag?business_id=1025853&shop_id=1025852&offer_id=10003272038252030632&offer_id=10001294836660478647'"
```
```
curl -XPOST "https://datacamp-admin.white.tst.vs.market.yandex.net/set_otrace_flag?business_id=1025853&shop_id=1025852&offer_id=10003272038252030632&offer_id=10001294836660478647&unset'
```

### GET /its_blame
Веб-страница с [построчным blame для ITS конфигов](https://datacamp-admin.white.vs.market.yandex.net/its_blame). Возвращает html страницу, поэтому можно ходить из браузера и не заучивать параметры.

### GET /its_history
Веб-страница с [историей изменения конфигов в ITS](https://datacamp-admin.white.vs.market.yandex.net/its_history). Возвращает html страницу, поэтому можно ходить из браузера и не заучивать параметры.

### GET /get_drop_filter
Получить текущее состояние дроп-фильтра

### PUT /set_drop_filter
Установить новое состояние дроп-фильтра (в формате json)

Пример запроса:
```
curl -X PUT "https://datacamp-admin.white.tst.vs.market.yandex.net/set_drop_filter" -d "{\"businessId\":[17,18],\"color\":\"pink\",\"dropSynthetic\":false,\"filterInside\":false}"
```
