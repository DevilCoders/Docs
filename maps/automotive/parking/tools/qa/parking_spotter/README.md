# parking_spotter


Инструмент запуска [parking_spotter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/lib/track_spotter) для данных, полученных в результате работы [split_sessions](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/tools/qa/split_sessions)


```
usage: parking_spotter [-L LOGLEVEL]

optional arguments:
  -L LOGLEVEL, --log-level LOGLEVEL
```

## Как запускать

Запустить в виде [YT-операции reduce](https://wiki.yandex-team.ru/yt/userdoc/operations/#reduce):


```
$> ya tool yt --proxy=hahn reduce \
        --job-count 1 \
        --binary ./parking_spotter \
        --src //home/maps/users/$(uuid)/sessions \
        --dst //home/maps/users/$(uuid)/parking_spotter \
        --input-format json \
        --output-format json \
        --local-file ./parking_spotter \
        --reduce-by device_id \
        --reduce-by session_start_timestamp \
        --sort-by device_id \
        --sort-by session_start_timestamp \
        --sort-by request_timestamp
```

Запустить локально:

```
$> ya tool yt --proxy=hahn read-table  \
    --format json //home/maps/users/$(uuid)/sessions | \
        ./parking_spotter -L debug > sessions.yt_json
```


