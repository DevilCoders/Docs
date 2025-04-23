# Enrich points in given table with additional info
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-enrich-adjusted [-h] [--sample-size SAMPLE_SIZE] [--yt-proxy YT_PROXY]`
    `input_path output_path map_driver_track --with-driver-status [fct_supply_state table or pattern] [--date DATE] `

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `input_path` path to intput directory (with adjusted_points).
* `output_path` path to output directory.
* `map_driver_track` path to directory with table with track_id, driver_uuid
