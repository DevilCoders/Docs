# Split split_sessions


Модуль для разрезания логов [parking-receiver'а](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_receiver) на на сессии. Описание алгоритма на [wiki](https://wiki.yandex-team.ru/automotive/serverdevelopment/projects/parkingv2/quality/detector/#predobrabotka)


```
usage: split_sessions [-h] [-l LIMIT] [-L LOGLEVEL] [-g SECONDS]

optional arguments:
  -h, --help            show this help message and exit
  -l LIMIT, --track-limit LIMIT
                        Limit track count to process
  -L LOGLEVEL, --log-level LOGLEVEL
                        Log level (debug, info, warning, error, critical)
  -g SECONDS, --split-timestamp-gap SECONDS
                        Timestamp gap threshold
```

### Как запускать в кластере

Модуль запускается как [YT Reduce](https://wiki.yandex-team.ru/yt/userdoc/operations/#reduce)


1. Создать табличку `//home/maps/users/<login>/tmp/split_sessions` со схемой из файла [split_sessions.schema](split_sessions.schema)

```
$> yt --proxy=hahn create --force table //home/maps/users/$(whoami)/tmp/split_sessions \
    --attributes "$(cat tools/qa/split_sessions/split_sessions.schema)"

```

2. Запустить YT операциию.


```
$> ya tool yt --proxy=hahn reduce \
        --job-count 3 \
        --binary ./split_sessions \
        --src //home/logfeller/logs/maps-auto-parking-receiver-testing-log/1d/2019-10-30 \
        --dst //home/maps/users/$(whoami)/tmp/split_sessions \
        --input-format json \
        --output-format json \
        --local-file tools/qa/split_sessions/split_sessions \
        --reduce-by device_id \
        --sort-by device_id \
        --sort-by _logfeller_timestamp

```

3. Сортировка результата по device_id,session_start_timestamp,request_timestamp


```
$> ya tool yt --proxy=hahn sort \
    --src //home/maps/users/$(whoami)/tmp/split_sessions \
    --dst //home/maps/users/$(whoami)/tmp/split_sessions_sorted \
    --sort-by device_id \
    --sort-by session_start_timestamp \
    --sort-by request_timestamp

```

### Как запустить локально

```
$> ya tool yt --proxy=hahn read-table  \
    --format json //home/logfeller/logs/maps-auto-parking-receiver-testing-log/1d/2019-10-30 | \
        ./tools/qa/split_sessions/split_sessions -L debug > sessions.yt_json
```


