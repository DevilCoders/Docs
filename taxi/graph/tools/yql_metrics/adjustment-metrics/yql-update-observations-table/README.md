# Remove data from table with date < `date`

Usage:
    `yql-update-observations-table [-h] [--yt-proxy YT_PROXY]`
    `input_eta_dir input_edge_chains_dir map_driver_track_dir output_dir [--date DATE]`

* `--yt-proxy` use cluster YT_PROXY for YT, default: hahn;
* `--date` data with date < [`date` - 6 days] will be removed. Default: (TODAY).
* `input_eta_dir` path to directory with eta_for_experiments table.
* `input_edge_chains_dir` path to directory with edge_chains_for_experiments table.
* `map_driver_track_dir` path to directory with (driver_id, track_id) table.
* `output_dir` path to observations table directory.
