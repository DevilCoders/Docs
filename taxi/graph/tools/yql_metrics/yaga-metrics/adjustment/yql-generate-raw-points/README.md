# Generate raw points
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-generate-raw-points [-h] [--yt-proxy YT_PROXY]`
    `[--input INPUT] [--drivers DRIVERS] [--date DATE]`
    `output_path`

* `--yt-proxy` use cluster `YT_PROXY` for YT, default: `hahn`;
* `--input` path to folder with raw points tables. Default: `//home/logfeller/logs/taxi-tracker-positions-log/1d`.
* ` --drivers` Path to table with driver ids. If given, only points for those drivers will be processed
* `--drivers-sample-size` If given, that percentage of drivers will be used.
* `--date` date for raw points in format `YYYY-MM-DD`. Default: previous day.
* `output_path` path to output folder. Table with name `raw_points` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
