# Filter sample points by business of driver
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-filter-samples [-h] [--yt-proxy YT_PROXY]`
    `drivers_info_table input_path output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `drivers_info_path` table with info about drivers business, pay attention to the date of table you are going to use. For example: `//home/taxi-dwh/cdm/supply/fct_supply_state_hist/2021-02-22`
* `input_path` path to folder with `sample_points` table. For example: `//home/taxi/home/zodiac/metrics/yql_metrics`;
* `output_path` path to output folder. Table with name `sample_points` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
