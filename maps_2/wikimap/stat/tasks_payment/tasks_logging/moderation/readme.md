Moderation Log
==============
[Calculates][calc description] moderation logs for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from `social.task_active`, `social.task_closed` and `social.commit_event` tables. These tables replicas can be found in Hahn cluster: [//home/maps/core/nmaps/dynamic/replica/social][replica].


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./moderation_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[calc description]: doc/calc_description.md
[replica]:          https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/social
[schema]:           /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
