# Graph coverage export
The worker for computing historical graph coverage by MRC photos and exporting it to ClickHouse.
It runs by cron and uses YT as an intermediate storage of computation results.
The resulting tables in ClickHouse are used to visualize graph coverage quality on stat charts.

Example command to manually run the worker for Moscow:
```
./tool/mrc-graph-coverage-export-tool \
    --config ../../libs/config/cfg/t-config.production.xml \
    --secret-version sec-01fjesdh3jykc9s87detcnw9mr \
    --output-yt-dir //tmp/$USER/mrc_stat \
    --road-graph /var/spool/yandex/maps/graph/19.01.23-1/ \
    --pedestrian-graph /var/spool/yandex/maps/graph/19.01.23-1/ \
    --geobase /var/cache/geobase/geodata6.bin \
    --bbox 37.422549,55.568474~37.858261,55.897237
```

The resulting tables in YT and ClickHouse have the following format:
### graph_coverage
Contains length of the coverage for individual road graph edges. Coverage length is stored along with the time span during which this coverage was valid.
| from_date | to_date | actualization_date | geo_id | fc  | is_toll | private_area | dataset | camera_deviation | length | graph_type |
| ---       | ---     | ---                | ---    | --- | ---     | ---          | ---     | ---              | ---    | ---        |

### graph_length
Contains aggregate length of the road graph edges grouped by geo_id and other attributes
| geo_id | fc  | is_toll | private_area | length | graph_type |
| ---    | --- | ---     | ---          | ---    | ---        |

### region
Contains mapping from geo_id to its name
| geo_id | name |
| ---    | ---  |


### graph_coverage_timeline

Table contains day-by-day values of graph coverage length sorted by date.

| date | fc  | is_toll | geo_id | private_area | graph_type | camera_deviation | dataset | age_catogory | length |
| ---  | --- | ---     | ---    | ---          | ---        | ---              | ---     | ---          | --- |
