Tasks Log
=========
Log contains assessable tasks performed at `date` matching log date. region\_id and task\_id are provided for each task. Moderation, feedback tasks and edits are taken into account.

Relies on [//home/maps/core/nmaps/analytics/feedback/db/feedback\_latest][feedback_latest] table and `social.commit_event`, `social.task` from [//home/maps/core/nmaps/dynamic/replica][replica]. Also uses [//home/maps/core/nmaps/analytics/geo-data/major\_regions\_map][major_regions_map].

Contains optimization that relies on assumption: all moderation tasks are expected to be closed in 14 days.

Usage
-----
This tool is a _nile cli udf_ with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for;
* `--proxy <cluster>` - cluster where calculations must be run;
* `--scale <scale>` - required by the RJM framework. Expected to be `daily` in this tool;
* `--use-yql` - yql backend should be used.

Usage example:

    ya nile ./udf/libassessment_tasks_log.so -- run --proxy hahn --scale daily --dates <dates> --use-yql


[feedback_latest]:      http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest
[major_regions_map]:    http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/geo-data/major_regions_map
[replica]:              http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/
