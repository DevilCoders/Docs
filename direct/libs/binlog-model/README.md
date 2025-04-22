# binlog-model - модель события в бинлоге 

BinlogEvent - это объект, который частично описывает событие из бинлога. В отличие от моделей из direct/libs/mysql-streaming, не пытается предоставить доступ ко всем данным из бинлога. В модели хранится только необходимый и достаточный набор данных для обработки бинлогов, благодаря чему сериализация модели эффективна.

В качестве бэкенда для сериализации используется protobuf.

Предполагается, что экземпляр BinlogEvent будет хранить в себе всю полезную информацию о
* Вставке строк
* Изменении строк
* Удалении строк
* Изменении схемы БД

В одной mysql-транзкции может быть несколько SQL-запросов. Один SQL-запрос может изменить несколько строк.
BinlogEvent содержит в себе информацию об изменениях из одного SQL-запроса. <b>NB:</b> Бывают запросы, которые изменяют миллионы строк. В таком случае один SQL-запрос может быть разбит на несколько BinlogEvent.

## Примеры

Запустить mysql для экспериментов с бинлогами можно через docker:
```bash
docker run \
    -ti \
    --rm \
    --name binlog \
    -e MYSQL_ALLOW_EMPTY_PASSWORD=1 \
    mysql:5.7 \
    --binlog-format=row \
    --binlog-row-image=noblob \
    --binlog-rows-query-log-events \
    --enforce-gtid-consistency \
    --gtid-mode=ON \
    --log-bin=binlog \
    --master-info-repository=TABLE \
    --server-id=12345
```

Смотреть в бинлоги можно командой `docker exec -ti binlog bash -c 'mysqlbinlog --verbose --verbose /var/lib/mysql/binlog.00000*'`, см. также man mysqlbinlog.

Предположим, БД относится к шарду ppc:1.

Ещё предположим, есть таблица:
```sql
CREATE DATABASE `ppc`;
USE `ppc`;
CREATE TABLE `campaigns` (
    `cid` int(10) unsigned NOT NULL PRIMARY KEY,
    `name` text,
    `currency` enum('RUB','UAH','KZT','USD','EUR','YND_FIXED','CHF','TRY','BYN') NOT NULL,
    `geo` text,
    `shows` int(10) DEFAULT NULL,
    `clicks` int(10) DEFAULT NULL
);
```

Также предположим, что мы должны всегда передавать значение currency, даже если оно не изменилось.

### Вставка строк

SQL-запрос:

```sql
INSERT INTO campaigns (cid, name, currency, geo, shows, clicks) 
VALUES (1, 'one', 'RUB', '', 0, 0),
    (2, 'two', 'USD', '10000,-123', 123, 456);
```

mysqlbinlog:
```
#180529  6:22:10 server id 12345  end_log_pos 823 CRC32 0x37c70027      GTID    last_committed=2        sequence_number=3       rbr_only=yes
/*!50718 SET TRANSACTION ISOLATION LEVEL READ COMMITTED*//*!*/;
SET @@SESSION.GTID_NEXT= '1d3a69ea-6308-11e8-b040-0242ac110002:8'/*!*/;
# at 823
#180529  6:22:10 server id 12345  end_log_pos 894 CRC32 0x84c2bf70      Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1527574930/*!*/;
BEGIN
/*!*/;
# at 894
#180529  6:22:10 server id 12345  end_log_pos 1064 CRC32 0x3dec1701     Rows_query
# INSERT INTO campaigns (cid, name, currency, geo, shows, clicks)
# VALUES (1, 'one', 'RUB', '', 0, 0),
#     (2, 'two', 'USD', '10000,-123', 123, 456)
# at 1064
#180529  6:22:10 server id 12345  end_log_pos 1124 CRC32 0x93a80462     Table_map: `ppc`.`campaigns` mapped to number 108
# at 1124
#180529  6:22:10 server id 12345  end_log_pos 1211 CRC32 0x1b04ad00     Write_rows: table id 108 flags: STMT_END_F

BINLOG '
kvEMWx05MAAAqgAAACgEAACAAJJJTlNFUlQgSU5UTyBjYW1wYWlnbnMgKGNpZCwgbmFtZSwgY3Vy
cmVuY3ksIGdlbywgc2hvd3MsIGNsaWNrcykgClZBTFVFUyAoMSwgJ29uZScsICdSVUInLCAnJywg
MCwgMCksCiAgICAoMiwgJ3R3bycsICdVU0QnLCAnMTAwMDAsLTEyMycsIDEyMywgNDU2KQEX7D0=
kvEMWxM5MAAAPAAAAGQEAAAAAGwAAAAAAAEAA3BwYwAJY2FtcGFpZ25zAAYD/P78AwMEAvcBAjpi
BKiT
kvEMWx45MAAAVwAAALsEAAAAAGwAAAAAAAEAAgAGP8ABAAAAAwBvbmUBAAAAAAAAAAAAAMACAAAA
AwB0d28ECgAxMDAwMCwtMTIzewAAAMgBAAAArQQb
'/*!*/;
### INSERT INTO `ppc`.`campaigns`
### SET
###   @1=1 /* INT meta=0 nullable=0 is_null=0 */
###   @2='one' /* BLOB/TEXT meta=2 nullable=1 is_null=0 */
###   @3=1 /* ENUM(1 byte) meta=63233 nullable=0 is_null=0 */
###   @4='' /* BLOB/TEXT meta=2 nullable=1 is_null=0 */
###   @5=0 /* INT meta=0 nullable=1 is_null=0 */
###   @6=0 /* INT meta=0 nullable=1 is_null=0 */
### INSERT INTO `ppc`.`campaigns`
### SET
###   @1=2 /* INT meta=0 nullable=0 is_null=0 */
###   @2='two' /* BLOB/TEXT meta=2 nullable=1 is_null=0 */
###   @3=4 /* ENUM(1 byte) meta=63233 nullable=0 is_null=0 */
###   @4='10000,-123' /* BLOB/TEXT meta=2 nullable=1 is_null=0 */
###   @5=123 /* INT meta=0 nullable=1 is_null=0 */
###   @6=456 /* INT meta=0 nullable=1 is_null=0 */
# at 1211
#180529  6:22:10 server id 12345  end_log_pos 1242 CRC32 0x748fe834     Xid = 9
COMMIT/*!*/;
```

Будет сгенерирован BinlogEvent с двумя Row.

* utcTimestamp = 2018-05-29 06:22:10
* source = "ppc:1"
* serverUuid = 1d3a69ea-6308-11e8-b040-0242ac110002
* transactionId = 8
* queryIndex = 0
* rowIndex = 0
* traceInfo = null
* db = "ppc"
* table = "campaigns"
* operation = INSERT
* rows
  1. Первый Row
    * rowIndex = 0
    * primaryKey =
      * cid = 1
    * before = []
    * after =
      * cid = (Long) 1
      * name = (String) "one"
      * currency = (String) "RUB"
      * geo = (String) ""
      * shows = (Integer) 0
      * clicks = (Integer) 0
  2. Второй Row
    * rowIndex = 1
    * primaryKey =
      * cid = 2
    * before = []
    * after =
      * cid = (Long) 2
      * name = (String) "two"
      * currency = (String) "USD"
      * geo = (String) "10000,-123"
      * shows = (Integer) 123
      * clicks = (Integer) 456
  
  
### Изменение строк

SQL-запрос:

```sql
UPDATE `campaigns` SET `geo` = NULL, `clicks` = 777 WHERE `cid` = 1; 
```

mysqlbinlog:
```
#180529  6:36:20 server id 12345  end_log_pos 1307 CRC32 0xa0770c57     GTID    last_committed=3        sequence_number=4       rbr_only=yes
/*!50718 SET TRANSACTION ISOLATION LEVEL READ COMMITTED*//*!*/;
SET @@SESSION.GTID_NEXT= '1d3a69ea-6308-11e8-b040-0242ac110002:9'/*!*/;
# at 1307
#180529  6:36:20 server id 12345  end_log_pos 1378 CRC32 0xc062d8f2     Query   thread_id=3     exec_time=0     error_code=0
SET TIMESTAMP=1527575780/*!*/;
SET @@session.pseudo_thread_id=3/*!*/;
SET @@session.foreign_key_checks=1, @@session.sql_auto_is_null=0, @@session.unique_checks=1, @@session.autocommit=1/*!*/;
SET @@session.sql_mode=1436549152/*!*/;
SET @@session.auto_increment_increment=1, @@session.auto_increment_offset=1/*!*/;
/*!\C latin1 *//*!*/;
SET @@session.character_set_client=8,@@session.collation_connection=8,@@session.collation_server=8/*!*/;
SET @@session.lc_time_names=0/*!*/;
SET @@session.collation_database=DEFAULT/*!*/;
BEGIN
/*!*/;
# at 1378
#180529  6:36:20 server id 12345  end_log_pos 1469 CRC32 0x4fae4e82     Rows_query
# UPDATE `campaigns` SET `geo` = NULL, `clicks` = 777 WHERE `cid` = 1
# at 1469
#180529  6:36:20 server id 12345  end_log_pos 1529 CRC32 0xf4a618b5     Table_map: `ppc`.`campaigns` mapped to number 108
# at 1529
#180529  6:36:20 server id 12345  end_log_pos 1593 CRC32 0x9df5b706     Update_rows: table id 108 flags: STMT_END_F

BINLOG '
5PQMWx05MAAAWwAAAL0FAACAAENVUERBVEUgYGNhbXBhaWduc2AgU0VUIGBnZW9gID0gTlVMTCwg
YGNsaWNrc2AgPSA3NzcgV0hFUkUgYGNpZGAgPSAxgk6uTw==
5PQMWxM5MAAAPAAAAPkFAAAAAGwAAAAAAAEAA3BwYwAJY2FtcGFpZ25zAAYD/P78AwMEAvcBAjq1
GKb0
5PQMWx85MAAAQAAAADkGAAAAAGwAAAAAAAEAAgAGNT3wAQAAAAEAAAAAAAAAAOQBAAAAAQAAAAAJ
AwAABrf1nQ==
'/*!*/;
### UPDATE `ppc`.`campaigns`
### WHERE
###   @1=1 /* INT meta=0 nullable=0 is_null=0 */
###   @3=1 /* ENUM(1 byte) meta=63233 nullable=0 is_null=0 */
###   @5=0 /* INT meta=0 nullable=1 is_null=0 */
###   @6=0 /* INT meta=0 nullable=1 is_null=0 */
### SET
###   @1=1 /* INT meta=0 nullable=0 is_null=0 */
###   @3=1 /* ENUM(1 byte) meta=63233 nullable=0 is_null=0 */
###   @4=NULL /* BLOB/TEXT meta=2 nullable=1 is_null=1 */
###   @5=0 /* INT meta=0 nullable=1 is_null=0 */
###   @6=777 /* INT meta=0 nullable=1 is_null=0 */
# at 1593
#180529  6:36:20 server id 12345  end_log_pos 1624 CRC32 0x6c346930     Xid = 21
COMMIT/*!*/;
```

Будет сгенерирован один BinlogEvent с одним Row:

* utcTimestamp = 2018-05-29 06:36:20
* source = "ppc:1"
* serverUuid = 1d3a69ea-6308-11e8-b040-0242ac110002
* transactionId = 9
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "campaigns"
* operation = UPDATE
* rows:
    * rowIndex = 0
    * primaryKey =
      * cid = 1
    * before =
      * currency = (String) "RUB"
    * after =
      * geo = null
      * clicks = (Integer) 777
  
  
### Удаление строк

SQL-запрос:

```sql
DELETE FROM `campaigns` WHERE `cid` = 2; 
```

mysqlbinlog:
```
#180529  6:38:57 server id 12345  end_log_pos 1689 CRC32 0x36ffc3dd     GTID    last_committed=4        sequence_number=5       rbr_only=yes
/*!50718 SET TRANSACTION ISOLATION LEVEL READ COMMITTED*//*!*/;
SET @@SESSION.GTID_NEXT= '1d3a69ea-6308-11e8-b040-0242ac110002:10'/*!*/;
# at 1689
#180529  6:38:57 server id 12345  end_log_pos 1760 CRC32 0x2e812c95     Query   thread_id=3     exec_time=0     error_code=0
SET TIMESTAMP=1527575937/*!*/;
SET @@session.pseudo_thread_id=3/*!*/;
SET @@session.foreign_key_checks=1, @@session.sql_auto_is_null=0, @@session.unique_checks=1, @@session.autocommit=1/*!*/;
SET @@session.sql_mode=1436549152/*!*/;
SET @@session.auto_increment_increment=1, @@session.auto_increment_offset=1/*!*/;
/*!\C latin1 *//*!*/;
SET @@session.character_set_client=8,@@session.collation_connection=8,@@session.collation_server=8/*!*/;
SET @@session.lc_time_names=0/*!*/;
SET @@session.collation_database=DEFAULT/*!*/;
BEGIN
/*!*/;
# at 1760
#180529  6:38:57 server id 12345  end_log_pos 1823 CRC32 0xd80f4fd5     Rows_query
# DELETE FROM `campaigns` WHERE `cid` = 2
# at 1823
#180529  6:38:57 server id 12345  end_log_pos 1883 CRC32 0x795ebfb9     Table_map: `ppc`.`campaigns` mapped to number 108
# at 1883
#180529  6:38:57 server id 12345  end_log_pos 1932 CRC32 0xe04d4913     Delete_rows: table id 108 flags: STMT_END_F

BINLOG '
gfUMWx05MAAAPwAAAB8HAACAACdERUxFVEUgRlJPTSBgY2FtcGFpZ25zYCBXSEVSRSBgY2lkYCA9
IDLVTw/Y
gfUMWxM5MAAAPAAAAFsHAAAAAGwAAAAAAAEAA3BwYwAJY2FtcGFpZ25zAAYD/P78AwMEAvcBAjq5
v155
gfUMWyA5MAAAMQAAAIwHAAAAAGwAAAAAAAEAAgAGNfACAAAABHsAAADIAQAAE0lN4A==
'/*!*/;
### DELETE FROM `ppc`.`campaigns`
### WHERE
###   @1=2 /* INT meta=0 nullable=0 is_null=0 */
###   @3=4 /* ENUM(1 byte) meta=63233 nullable=0 is_null=0 */
###   @5=123 /* INT meta=0 nullable=1 is_null=0 */
###   @6=456 /* INT meta=0 nullable=1 is_null=0 */
# at 1932
#180529  6:38:57 server id 12345  end_log_pos 1963 CRC32 0xdccae506     Xid = 22
COMMIT/*!*/;
```

Будет сгенерирован один BinlogEvent с одним Row:

* utcTimestamp = 2018-05-29 06:38:57
* source = "ppc:1"
* serverUuid = 1d3a69ea-6308-11e8-b040-0242ac110002
* transactionId = 10
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "campaigns"
* operation = DELETE
* rows
    * rowIndex = 0
    * primaryKey =
      * cid = 2
    * before =
      * currency = (String) "USD"
    * after = []

### Создание таблицы

SQL-запрос:
```sql
CREATE TABLE foobar (foo int not null primary key, bar int null)
```

mysqlbinlog:
```
#180606  8:13:02 server id 12345  end_log_pos 417 CRC32 0xd53388df      GTID    last_committed=1        sequence_number=2       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:7'/*!*/;
# at 417
#180606  8:13:02 server id 12345  end_log_pos 541 CRC32 0xdc72d2f6      Query   thread_id=2     exec_time=0     error_code=0
use `ppc`/*!*/;
SET TIMESTAMP=1528272782/*!*/;
CREATE TABLE foobar (foo int not null primary key, bar int null)
/*!*/;
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 08:13:02
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 7
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * CreateTable
    * columns:
      * 0:
        * columnName = "foo"
        * columnType = INTEGER
        * nullable = false
      * 1:
        * columnName = "bar"
        * columnType = INTEGER
        * nullable = true
    * primaryKey:
      * foo
    
Событие создания таблицы никогда не разбивается на несколько BinlogEvent.
  
### Изменение колонки

SQL-запрос
```sql
alter table foobar modify column bar int not null
```

mysqlbinlog:
```
#180606  8:16:50 server id 12345  end_log_pos 606 CRC32 0x48e44d16      GTID    last_committed=2        sequence_number=3       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:8'/*!*/;
# at 606
#180606  8:16:50 server id 12345  end_log_pos 727 CRC32 0xdb791b4a      Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1528273010/*!*/;
alter table foobar modify column bar int not null
/*!*/;
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 08:16:50
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 8
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * CreateOrModifyColumn
    * columnName = "bar"
    * columnType = INTEGER
    * nullable = false
    
### Добавление колонки

SQL-запрос
```sql
alter table foobar add column baz text not null
```

mysqlbinlog:
```
#180606  8:22:13 server id 12345  end_log_pos 792 CRC32 0x805c2973      GTID    last_committed=3        sequence_number=4       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:9'/*!*/;
# at 792
#180606  8:22:13 server id 12345  end_log_pos 911 CRC32 0x31e074f7      Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1528273333/*!*/;
alter table foobar add column baz text not null
/*!*/;
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 08:22:13
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 9
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * CreateOrModifyColumn
    * columnName = "baz"
    * columnType = STRING
    * nullable = false
    
### Переименование колонки

SQL-запрос
```sql
alter table foobar change column baz hurrdurr text not null
```

mysqlbinlog:
```
#180606 11:17:27 server id 12345  end_log_pos 976 CRC32 0x4e108ebb      GTID    last_committed=4        sequence_number=5       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:10'/*!*/;
# at 976
#180606 11:17:27 server id 12345  end_log_pos 1107 CRC32 0x1d52709c     Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1528283847/*!*/;
alter table foobar change column baz hurrdurr text not null
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 11:17:27
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 10
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * RenameColumn
    * oldColumnName = "baz"
    * newColumnName = "hurrdurr"


### Удаление колонки

SQL-запрос
```sql
alter table foobar drop column hurrdurr
```

mysqlbinlog
```
#180606 11:20:21 server id 12345  end_log_pos 1172 CRC32 0x25ff074f     GTID    last_committed=5        sequence_number=6       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:11'/*!*/;
# at 1172
#180606 11:20:21 server id 12345  end_log_pos 1283 CRC32 0xf7d31aaa     Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1528284021/*!*/;
alter table foobar drop column hurrdurr
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 11:20:21
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 11
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * DropColumn
    * columnName = "hurrdurr"
    
    
### Удаление таблицы

SQL-запрос
```sql
drop table foobar
```

mysqlbinlog
```
#180606 11:21:58 server id 12345  end_log_pos 1348 CRC32 0x081880f8     GTID    last_committed=6        sequence_number=7       rbr_only=no
SET @@SESSION.GTID_NEXT= '495bea6a-6961-11e8-abee-0242ac110003:12'/*!*/;
# at 1348
#180606 11:21:58 server id 12345  end_log_pos 1465 CRC32 0x37fdc26d     Query   thread_id=2     exec_time=0     error_code=0
SET TIMESTAMP=1528284118/*!*/;
DROP TABLE `foobar` /* generated by server */
```

Будет сгенерирован один BinlogEvent:

* utcTimestamp = 2018-06-06 11:21:58
* source = "ppc:1"
* serverUuid = 495bea6a-6961-11e8-abee-0242ac110003
* transactionId = 12
* queryIndex = 0
* traceInfo = null
* db = "ppc"
* table = "foobar"
* operation = SCHEMA
* schemaChanges
  * DropTable
