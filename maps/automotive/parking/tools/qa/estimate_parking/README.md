# estimate_parking

Инструмент оценки работы [parking_spotter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/lib/track_spotter) на эталонных данных.

```
usage: estimate_parking [-L LOGLEVEL] files

optional arguments:
  -L LOGLEVEL, --log-level LOGLEVEL
```

## Данные для оценки

Эталонные данные для оценки добавляются вручную в csv файл, на основе визуального анализа трека.
Формат - CSV

* `device_id`
* `session_start_timestamp`
* `Latitude`
* `Longitude`
* `parking_timestamp`

## Как запускать

```
$> ya tool yt --proxy=hahn read-table  \
    --format json //home/maps/users/$(uuid)/sessions | \
        ./estimate_parking -L debug check.csv
```

## Пример как выбрать данные за несколько дней для device_id

```
use hahn;
PRAGMA yt.InferSchema;
INSERT INTO `home/maps/users/$(uuid)/sessions`
WITH TRUNCATE
SELECT *
FROM RABGE(`home/maps/users/$(uuid)/sessions`,`2019-11-08`,`2019-11-11`)
WHERE `device_id` == "6ef..."
ORDER BY `device_id`, `session_start_timestamp`, `request_timestamp`;
```
