Assessment Log
==============
Calculates assessment logs for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from the following tables:
- [//home/maps/core/nmaps/analytics/feedback/db/feedback\_latest][feedback];
- [//home/maps/core/nmaps/dynamic/replica][replica]:
  - `assessment/assessment_grade`;
  - `assessment/assessment_unit`;
  - `social/social_commit_event`;
  - `social/social_task_active`;
  - `social/social_task_closed`;
- [//home/startrek/tables/prod/yandex-team/queue/maps-pw][maps-pw]:
  - `issues`;
  - `components`.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./assessment_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[feedback]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest
[maps-pw]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/startrek/tables/prod/yandex-team/queue/maps-pw
[replica]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica
[schema]:   /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
