# Schools road event xml generator
Generates schools road events xml, suitable for infpoints legacy import. Outputs result to stdout. Uses yt table as input. Input table must have `lon`, `lat` and `trait` columns. Any two road events must not have equal `lon` and `lat` values at the same time, because road event's uuid is calculated based on it's position, thus same position leads to duplicate uuids.
## Options
* `-r, --road-event-table` - path to input yt table in `hahn` cluster;
* `-l, --road-events-count-limit` - output road events count limit;
* `-e, --exclude-trait` - trait to exclude, if road event has specified value in `trait` column, it won't be added to output xml, this option can be specified multiple times to exclude multiple traits.
### Usage example
`./school_road_event_xml_generator -r '//home/SOME_DIR/road_event' -l 100 -e too_far_on_foot -e regulated_by_traffic_light > schools.xml` - will output to `schools.xml` not more than 100 road events with 'school' tag that don't have traits `"too_far_on_foot"` or `"regulated_by_traffic_light"`.
