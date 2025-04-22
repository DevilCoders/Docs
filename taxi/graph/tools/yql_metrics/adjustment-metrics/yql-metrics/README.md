# Calculate metrics (ETA or edge ids) between reference values and adjusted values.
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-metrics [-h] [--yt-proxy YT_PROXY]`
    `reference_path adjusted_path output_path`
    `[--with-ab-table]`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--with-ab-table` insert data to ab table (for evaluating observations table);
* `reference_path` Path to table with reference values, for example: `//home/taxi/home/zodiac/metrics/yql_metrics/ref_eta`.
* `test_path` Path to table with test values. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/test_eta`.
* `output_path` Path to output folder. Table with name `[type]_metrics` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.