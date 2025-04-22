# Calculate ETA for tracks from input adjusted table and destination points table.
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-eta [-h] [--yt-proxy YT_PROXY]`
    `graph_path adjusted_table destination_points output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `graph_path` Path to folder with graph, for example: `//home/maps/graph/19.06.09-0`.
* `adjusted_path` Path to table with adjusted_tracks, for example: `//home/taxi/home/zodiac/metrics/yql_metrics/output/adjusted_full`.
* `destination_points` Path to table with destination_points. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/destination_points`.
* `output_path` Path to output folder. Table with name `[adjusted_table_name]_eta` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
