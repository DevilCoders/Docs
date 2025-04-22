OSM hypotheses (roads-d1)
===

| Key | Value |
| --- | --- |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/74577 |
| Output tables | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/production/geoq-hypotheses/roads-d1 |

#### Something broken?

Contact ([or create a ticket](https://st.yandex-team.ru/createTicket?queue=GEOQ)) [GEOQ](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) ([Slack helpline channel](https://yndx-all.slack.com/archives/C01RN8Z27MX)).

Description
---

Calculates hypotheses using OSM road graph differences (are uploaded regularly and [stored here](//home/maps/core/nmaps/production/osm-diffs)) in form of polylines. Algorithm tries to find similar geometries in our road graph using different statistics (like a polylines distance) and if it fails to find any, it reports it to nmaps.

Help
---

```
~/arcadia/maps/geoq/hypotheses/bin/osm/road_graph_diff/yt$ ./yt --help
usage: yt [-h] [-i [INPUT_TABLES [INPUT_TABLES ...]]] [-o OUTPUT_TABLE]
          [--memory-limit MEMORY_LIMIT] [--job-count JOB_COUNT] [-p PROXIMITY]
          [-t THRESHOLD] [--store-locally]
          [--exclude-types [EXCLUDE_TYPES [EXCLUDE_TYPES ...]]]
          [--exclude-operations [EXCLUDE_OPERATIONS [EXCLUDE_OPERATIONS ...]]]
          [-v] [--host HOST] [--source-name SOURCE_NAME] [--tmp-path TMP_PATH]

Process OSM diff tables.

optional arguments:
  -h, --help            show this help message and exit
  -i [INPUT_TABLES [INPUT_TABLES ...]], --input-tables [INPUT_TABLES [INPUT_TABLES ...]]
                        input tables with roads diff data
  -o OUTPUT_TABLE, --output-table OUTPUT_TABLE
                        output table with hypotheses
  --memory-limit MEMORY_LIMIT
                        memory limit in GB
  --job-count JOB_COUNT
                        YT job count.
  -p PROXIMITY, --proximity PROXIMITY
                        snap proximity in meters
  -t THRESHOLD, --threshold THRESHOLD
                        join threshold in meters
  --store-locally       store resulting table locally or otherwise upload it to
                        YT
  --exclude-types [EXCLUDE_TYPES [EXCLUDE_TYPES ...]]
                        set road types to be excluded
  --exclude-operations [EXCLUDE_OPERATIONS [EXCLUDE_OPERATIONS ...]]
                        set operations to be excluded
  -v, --verbose         print out additional information
  --host HOST           host to upload hypotheses
  --source-name SOURCE_NAME
                        hypotheses source name
  --tmp-path TMP_PATH   path where to store tmp tables

```