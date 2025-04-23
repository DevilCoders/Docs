Tracker Test Log
================
Calculates tasks logs based on tickets from [GEOTESTPW queue][geotestpw] for the provided dates.

The log is generated from the [replica] of the GEOTESTPW queue on YT Hahn cluster.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./tracker_geotest_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[geotestpw]: https://st.yandex-team.ru/GEOTESTPW
[replica]:   https://yt.yandex-team.ru/hahn/navigation?path=//home/startrek/tables/prod/yandex-team/queue/GEOTESTPW
