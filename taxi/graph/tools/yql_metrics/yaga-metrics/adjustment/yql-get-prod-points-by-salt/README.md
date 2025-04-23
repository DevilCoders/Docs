# Get adjusted on production points respective to sample points.
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-get-respective-prod-points [-h] [--yt-proxy YT_PROXY] [--input-table table] [--input-daily-dir dir] [--date date]`
    `input_path  output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--input-table` path to table with adjusted points on production.
* `--input-daily-dir` path to directory with adjusted points on production, default: `//home/logfeller/logs/taxi-yaga-metrolog-edge-positions-log/1d`
* `--date` date for table with adjusted points on production. Use it with `--input-daily-dir`
* `adjusted_table` Path to table with sample_points, for example: `//home/taxi/home/zodiac/metrics/yql_metrics/output/sample_points`.
* `output_path` Path to output folder. Table with name `adjusted_points` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
