# **Calculate time-shifted points based on track.

Usage:
    `yql-eta [-h] [--yt-proxy YT_PROXY]`
    `--adjusted_table --output_path`
    `--predict_time --window_size`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--adjusted_table` Path to table with adjusted_tracks and adjusted_points, for example: `//home/taxi/home/zodiac/metrics/yql_metrics/output/adjusted_slice`.
* `--output_path` Path to output folder. Table with name `[adjusted_table_name]_eta` will be overwritten. For example: `//home/taxi/home/zodiac/metrics/yql_metrics/output`.
* `--predict_time` Horizon of prediction in seconds.
* `--window_size` Window in which we are looking for shifted point `[timestamp + --predicted_time - --window_size; timestamp + --predicted_time + --window_size]`