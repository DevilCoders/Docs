# Назначение

Скрипт запускает параметризованный датой yql-запрос.
Запрос декодирует и трансфомирует данные в удобный для последующего
анализа формат.

Результат тут: `//home/vipplanners/cooked_awaps/`


## Таблицы

* `mini/%Y-%m-%d` - короткая версия с полезными actionid (0, 1, 52, 53, 54, 55, 56, 57, 58, 62, 63, 83, 88, 89, 90), без столбцов с массивами для placementid > 1.
  Для истории за больший период
* `ext/%Y-%m-%d` - полная версия
* `dsp/%Y-%m-%d` - списания победителей (для мп по rtb-событиям)
* `other/ext_errors` - количество строк с null и ошибками декодирования накаждый день в `ext/*` с группировкой по actionid.

### Описание столбцов

- timestamp — время события в UTC

### История изменений
- 2018-01-01
  * `global_request_id` из awaps в ext
  * `rtb_bid_price` из awaps в ext, mini, ext_errors
  * `dsp_realprice` (`realprice`) в dsp
- 2017-09-01 Изменился соц.дем. Повились `sd_age_45_55`, `sd_age_56_plus`; перестал существовать `sd_age_45`. Вместо вероятностей всегда 100% у одного из сегментов. Логика порогов осталась за Криптой.
- 2017-08-27 поле `timestamp` c unixtime стало вычисляться из поля `iso_eventtime`.

## Установка и запуск

Используется бинарник `yql` в домашнем каталоге пользователя и установленный [`yt`](https://wiki.yandex-team.ru/yt/userdoc/pythonwrapper/)

```bash
$ cd && git clone https://github.yandex-team.ru/n-bar/cooked-logs.git && cd cooked-logs/awaps
# обычный запуск на дату
./yql/run 2017-03-05
# запуск в фоне
./yql/run 2017-03-05 &> /dev/null &
# запуск последовательно для списка дат
./missed_dates | xargs -L 1 ./yql/run &> /dev/null &
# запуск в кроне
1 2,5 * * * cd ~/cooked-logs/awaps && ./croned_yql.sh
```
## Misc

Удалить конкретный месяц:
```bash
$ yt list '//home/vipplanners/cooked_awaps/ext' | grep '2017-10' | xargs -P1 -L1 -I{} yt remove "//home/vipplanners/cooked_awaps/ext/{}"
```

## ClickHouse
### Пример схемы

Таблицы можно без изменений переложить в ClickHouse. Например так:

```sql
-- На каждый день своя таблица
CREATE TABLE `2017-02-14`
(
 `has_coord`        Int8    DEFAULT -1,
 `timestamp`        UInt64  DEFAULT 0,
 `event_date`       MATERIALIZED toDate(`timestamp` / 1e6),
 `event_date_time`  ALIAS toDateTime(`timestamp` / 1e6),
 `userid`           UInt64  DEFAULT 0,
 `user_id_type`     Int8    DEFAULT -1,
 `yandexuid`        UInt64  DEFAULT 0,
 `adid`             Int32   DEFAULT -1,
 `placementid`      Int32   DEFAULT -1,
 `mime_type`        Int8    DEFAULT -1,
 `height`           Int16   DEFAULT -1,
 `width`            Int16   DEFAULT -1,
 `actionid`         Int16   DEFAULT -1,
 `geo_zone`         Int32   DEFAULT 10000,
 `rtb_request_id`   UInt64  DEFAULT 0,
 `dsp_price`        Int64   DEFAULT -1,
 `rtb_resource_id`  Int32   DEFAULT -1,
 `rtb_host_id`      Int16   DEFAULT -1,
 `sectionid`        Int32   DEFAULT -1,
 `lon`              Float64 DEFAULT nan,
 `lat`              Float64 DEFAULT nan,
 `rtb_stlm_price`   Int32   DEFAULT -1,
 `is_mobile`        Int8    DEFAULT -1,
 `is_tablet`        Int8    DEFAULT -1,
 `os_family`        String  DEFAULT '',
 `device_vendor`    String  DEFAULT '',
 `bandwidth`        Int32   DEFAULT -1,
 `user_regular_location_lat` Array(Float64) DEFAULT emptyArrayFloat64(),
 `user_regular_location_lon` Array(Float64) DEFAULT emptyArrayFloat64(),
 `user_search_cats`  Array(UInt32) DEFAULT emptyArrayUInt32(),
 `user_adhoc_prob`   Array(UInt32) DEFAULT emptyArrayUInt32(),
 `user_adhoc_strict` Array(UInt32) DEFAULT emptyArrayUInt32(),
 `user_goals`        Array(UInt32) DEFAULT emptyArrayUInt32(),
 `sd_gender`         Int8          DEFAULT -1,
 `sd_age`            Int8          DEFAULT -1,
 `sd_income`         Int8          DEFAULT -1
) ENGINE = MergeTree(event_date, intHash32(userid), (has_coord, sectionid, rtb_resource_id, intHash32(userid)), 8192);

-- Отображение для запросов на чтение
CREATE TABLE mediastat_v
(
...
) ENGINE = Merge(default, '^[0-9]{4}(-[0-9][0-9]){2}$');
```

### YT -> CH
Источник `//home/vipplanners/cooked_awaps/ext/%Y-%m-%d`

Один поток:
```bash
yt read '//home/vipplanners/cooked_awaps/ext/2017-03-01[#1]' --format=json | \
clickhouse-client --query='INSERT INTO `2017-03-01` FORMAT JSONEachRow'
```

Несколько потоков:
```bash
./clickhouse/create_table 2017-02-14 && \
./bounds 2017-02-14 | \
xargs -L 1 -P 10 ./clickhouse/insert &> /dev/null &
```