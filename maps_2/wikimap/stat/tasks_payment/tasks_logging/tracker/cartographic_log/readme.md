Tracker Cartographic Log
========================
Calculates tasks logs based on tickets from [MAPSPW], [FEEDBACKPW] and [OUTKARTPW] queues for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from the queues [replica] on YT Hahn cluster.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./tracker_cartographic_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily

This tool checks Tracker [replica] freshness. To disable this check and force calculation on possibly non full data `--skip-tracker-replica-freshness-check` can be used.


[feedbackpw]: https://st.yandex-team.ru/FEEDBACKPW
[mapspw]:     https://st.yandex-team.ru/MAPSPW
[outkartpw]:  https://st.yandex-team.ru/OUTKARTPW

[replica]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/startrek/tables/prod/yandex-team/queue/maps-pw
[schema]:     /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
