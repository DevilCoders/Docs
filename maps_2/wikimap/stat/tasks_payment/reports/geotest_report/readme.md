Tasks Payment GeoTest Report
============================
Calculates [Tasks Payment GeoTest Report][report] for the provided dates.

The report is generated from [logs], [staff dump] and [tariffs].


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the report must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - only `daily` scale is supported.

Usage example:

    ./tasks_payment_geotest_report run --proxy hahn --scale daily --dates 2020-01-25 2020-01-26


Report Publishing
-----------------
By default, generated report is published on [stat-beta.yandex-team.ru][beta report]. To publish this report on [stat.yandex-team.ru][report] `--publish-production` parameter must be used.


[staff dump]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[logs]:        https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-qa/analytics/tasks_payment/tasks_logs
[tariffs]:     https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-qa/analytics/tasks_payment/dictionaries/task_tariff_map

[beta report]: https://stat-beta.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment_GeoTest
[report]:      https://stat.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment_GeoTest
