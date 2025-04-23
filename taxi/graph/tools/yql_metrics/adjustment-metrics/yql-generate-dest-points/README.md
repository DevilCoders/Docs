# Generate destination points from tracks
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-generate-dest-points [-h] [--yt-proxy YT_PROXY]`
    `input_path output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `input_path` path to folder with `raw_tracks` table. For example: `//home/taxi/home/zodiac/metrics/yql_metrics`;
* `output_path` path to output folder. Table with name `destination_points` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
