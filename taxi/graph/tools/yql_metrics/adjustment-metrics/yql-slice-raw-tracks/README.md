# Make sliced tracks from raw points and sample
More info: [YQL metrics](https://wiki.yandex-team.ru/taxi/backend/graph/adjust-driver/metrics/).

Usage:
    `yql-slice-raw-tracks [-h] [--backward BACKWARD] [--forward FORWARD] [--yt-proxy YT_PROXY]`
    `input_path output_path`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--backward` number of points before selected one;
* `--forward` number of points after selected one;
* `input_path` path to folder with `raw_tracks` and `slice_tracks` tables. For example: `//home/taxi/home/zodiac/metrics/yql_metrics`;
* `output_path` path to output folder. Table with name `sample_tracks` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
