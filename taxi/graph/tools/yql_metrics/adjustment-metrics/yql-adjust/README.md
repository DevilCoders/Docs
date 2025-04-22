# Adjust tracks using graph and table with points
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-adjust [-h] [--adjust-prob] [--yt-proxy YT_PROXY]`
    `(--config-online | --config-offline | --config CONFIG)`
    `graph_path path output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--adjust-prob` use probability adjusting instead if set;
* `--config-online | --config-offline | --config CONFIG` use pre-installed config or external config with path `CONFIG`;
* `graph_path` Path to folder with graph, for example: `//home/maps/graph/19.06.09-0`;
* `path` Path to track_slice table. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/track_slice`;
* `output_path` Path to output folder. All tables at this path will be removed. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
