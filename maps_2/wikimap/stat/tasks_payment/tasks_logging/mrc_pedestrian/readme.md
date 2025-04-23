MRC Pedestrian Log
============
Calculates mrc pedestrian logs for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from [`signals_walk_object_replica`][signals_walk_object_replica], [`feedback_dump`][feedback_dump]
and [`mrc_pedestrian_region_log`][mrc_pedestrian_region_log] tables.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./mrc_pedestrian_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[signals_walk_object_replica]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/mrc/signals_walk_object
[feedback_dump]:               https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest
[mrc_pedestrian_region_log]:   https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/logs/mrc-pedestrian-region-log
[schema]:                      /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
