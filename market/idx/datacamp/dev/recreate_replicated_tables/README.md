## Datacamp tables modification tool

### Пересоздание мета-таблицы

Пересоздание мета-таблицы с решардированием и обновлением реплик.

Применимость:
- решардирование мета-таблицы
- если все сломалось и нужно срочно восстановить работоспособность

Пример использования:
```
export YT_TOKEN_PATH=/etc/datasources/yt-market-indexer
./datacamp_tables --config ../conf/testing --env testing --mode recreate --table service_offers
```

### Создание/обновление реплицированной таблицы

Создает мета-таблицу с репликами или обновляет схему таблиц, если устанавливаемая схема отличается от текущей схемы
мета-таблицы.

Применимость:
- обновить описание прото-колонок (_yql_proto_field_)
- добавить колнку в таблицу (приводит к пересозданию мета-таблицы на новой схеме и перемаунчиванию таблиц реплик с
  добавлением новых колонок)

Пример использования:
```
export YT_TOKEN_PATH=/etc/datasources/yt-market-indexer
./datacamp_tables --config ../conf/testing --env testing --mode update --table service_offers
```

Для поисковых таблиц используются конфиги search_testing/search_production

### Принудительное обновление реплицированной таблицы

Запускает процесс обновления схем таблиц, даже если устанавливаемая схема не отличается от текущей схемы мета-таблицы.

Применимость:
- если запуск в режиме update завершился ошибкой, но схема мета-таблицы уже успела обновиться

Пример использования:
```
export YT_TOKEN_PATH=/etc/datasources/yt-market-indexer
./datacamp_tables --config ../conf/testing --env testing --mode force_update --table service_offers
```

### Важно
Для таблиц свежих офферов ```fresh``` нужно использовать конфиги ```conf/mr_*```

### Возможные ошибки
```
INFO: 2021-03-05 15:16:02.164 +0300 YtHelpers.cpp:182 Trying to unmount //home/market/production/indexer/datacamp/united/actual_service_offers
ERROR: 2021-03-05 15:16:02.210 +0300 YtReplicatedTable.cpp:247 (NYT::TErrorResponse) 'Cannot change table schema since some tablets are in transient state'; full error: {"code"=1706;"message"="Cannot change table schema since some tablets are in transient state";"attributes"={"fid"=18431153676808877671u;"expected_tablet_state"="mounted";"tid"=13992606429535465908u;"last_mount_transaction_id"="22b95-11a636-3fe0001-5a07";"datetime"="2021-03-05T12:16:02.201003Z";"pid"=243;"host"="m002-hahn.sas.yp-c.yandex.net"}}
```
Оживить таблицу поможет перезапуск в режиме recreate или force_update
