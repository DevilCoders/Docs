#Build table from pricing tables
This utility build result table from pricing tables. Result table columns: | order_id | caller_link |
link | uuid | route_points | route_time | route_distance | route_timestamp | pred_points | pred_time |
pred_distance | pred_timestamp |. YT Proxy is `hahn`.

Usage: `yql-build-pricing-tables [--yt-proxy YT_PROXY] date_from date_to output_path`

* `--yt-proxy` - use cluster YT_PROXY for YT, default: hahn;
* `date_from` - YYYY-MM-DD string
* `date_to` - YYYY-MM-DD string
* `output_path` - path on YT for writing result table. For example: `home/taxi/home/zodiac/metrics/yql_metrics/output`.