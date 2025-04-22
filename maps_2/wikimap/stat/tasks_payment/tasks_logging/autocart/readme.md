Autocart Log
============
Calculates autocart logs for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from [`assessors`][assessors] and [`nmaps-users-dump-log`][nmaps-users-dump-log] tables.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./autocart_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[assessors]:            https://yt.yandex-team.ru/hahn/navigation?path=//home/maps_mrc/domovoi/storage/assessors
[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[schema]:               /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
