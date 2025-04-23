Install
---------------------
```bash
virtualenv env
. env/bin/activate
pip install -U pip
pip install --upgrade --ignore-installed setuptools
git clone https://github.yandex-team.ru/B2BGeo/analytics.git #
cd analytics/geo-analytics
pip install -i https://pypi.yandex-team.ru/simple .
experiment --help
```

Experiment
---------------------
```bash
experiment --help
usage: experiment [-h] [--date-format DATE_FORMAT]
                  (--src-tables SRC_TABLES [SRC_TABLES ...] | --src-node SRC_NODE)
                  [--already-mapped] [--id-column ID_COLUMN]
                  [--timestamp-column TIMESTAMP_COLUMN]
                  [--latitude-column LATITUDE_COLUMN]
                  [--longitude-column LONGITUDE_COLUMN] [--yt-proxy YT_PROXY]
                  [--yt-token YT_TOKEN] [--yt-pool YT_POOL]
                  [--job-count JOB_COUNT]
                  [--data-size-per-job DATA_SIZE_PER_JOB]
                  [--memory-limit MEMORY_LIMIT]
                  [--short-interaction-r SHORT_INTERACTION_R]
                  [--continuous-interaction-r CONTINUOUS_INTERACTION_R]
                  [--si-before-loss-r SI_BEFORE_LOSS_R]
                  [--min-continuous-interaction-time MIN_CONTINUOUS_INTERACTION_TIME]
                  [--max-continuous-interaction-time MAX_CONTINUOUS_INTERACTION_TIME]
                  [--event-timeout EVENT_TIMEOUT]
                  [--min-track-timeout-after-loss MIN_TRACK_TIMEOUT_AFTER_LOSS]
                  [--min-time-in-si-r-before-loss MIN_TIME_IN_SI_R_BEFORE_LOSS]
                  --start-time START_TIME --end-time END_TIME
                  [--time-delta TIME_DELTA] [--coord-delta COORD_DELTA]
                  [--geoindex-precision GEOINDEX_PRECISION]
                  (--local-index-path LOCAL_INDEX_PATH | --remote-index-path REMOTE_INDEX_PATH)
                  --result-node RESULT_NODE --result-name RESULT_NAME
                  [--store-mapped] [--store-events]
                  [--calc-directed-interactions]

optional arguments:
  -h, --help            show this help message and exit
  --date-format DATE_FORMAT

src:
  --src-tables SRC_TABLES [SRC_TABLES ...]
  --src-node SRC_NODE
  --already-mapped      assumes src-tables already have been mapped to points
                        (have nearest_points column). calculation process will
                        start from event extraction (default: False)
  --id-column ID_COLUMN
  --timestamp-column TIMESTAMP_COLUMN
  --latitude-column LATITUDE_COLUMN
  --longitude-column LONGITUDE_COLUMN

yt:
  yt parameters

  --yt-proxy YT_PROXY
  --yt-token YT_TOKEN
  --yt-pool YT_POOL
  --job-count JOB_COUNT
  --data-size-per-job DATA_SIZE_PER_JOB
  --memory-limit MEMORY_LIMIT

events:
  events extraction parameters

  --short-interaction-r SHORT_INTERACTION_R
  --continuous-interaction-r CONTINUOUS_INTERACTION_R
  --si-before-loss-r SI_BEFORE_LOSS_R
  --min-continuous-interaction-time MIN_CONTINUOUS_INTERACTION_TIME
  --max-continuous-interaction-time MAX_CONTINUOUS_INTERACTION_TIME
  --event-timeout EVENT_TIMEOUT
                        minimum time interval between users events for certain
                        point (default: 43200)
  --min-track-timeout-after-loss MIN_TRACK_TIMEOUT_AFTER_LOSS
                        Min time interval w/o events after loss while
                        detecting short_interaction_before_loss (default: 90)
  --min-time-in-si-r-before-loss MIN_TIME_IN_SI_R_BEFORE_LOSS
                        Min time interval in short interaction radius before
                        loss while detecting short_interaction_before_loss
                        (default: 15)

experiment:
  --start-time START_TIME
  --end-time END_TIME
  --time-delta TIME_DELTA
                        will be used while filtering raw log by time (default:
                        300)
  --coord-delta COORD_DELTA
                        will be used while filtering raw log by bbox.
                        bbox=[(min_lat - coord_delta, min_lon - coord_delta),
                        (max_lat + coord_delta, max_lon + coord_delta)]
                        (default: 0.2)
  --geoindex-precision GEOINDEX_PRECISION
                        See https://github.com/gusdan/geoindex for details
                        (default: 6)
  --local-index-path LOCAL_INDEX_PATH
  --remote-index-path REMOTE_INDEX_PATH

result:
  --result-node RESULT_NODE
  --result-name RESULT_NAME
  --store-mapped
  --store-events
  --calc-directed-interactions
  ```

Set read schema (YQL)
---------------------
```bash
set-read-schema --help
usage: set-read-schema [-h] [--yt-proxy YT_PROXY] [--yt-token YT_TOKEN]
                       --read-schema READ_SCHEMA
                       [--src-tables SRC_TABLES [SRC_TABLES ...] | --src-node
                       SRC_NODE]

optional arguments:
  -h, --help            show this help message and exit
  --yt-proxy YT_PROXY
  --yt-token YT_TOKEN
  --read-schema READ_SCHEMA
                        '{"column": "type"}'
  --src-tables SRC_TABLES [SRC_TABLES ...]
  --src-node SRC_NODE
```
