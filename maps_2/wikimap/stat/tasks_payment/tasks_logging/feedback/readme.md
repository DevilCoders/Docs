Feedback Log
============
Calculates feedback tasks logs for the provided dates in the [unified][schema] to other payment tasks form.

The log is generated from:
- table produced by [`dump_feedback_to_yt`][dump_feedback_to_yt] tool, which can be found in Hahn cluster: [//home/maps/core/nmaps/analytics/feedback/db][feedback_table];
- [`social.commit_event`][social.commit_event] replica.


Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the log must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Usage example:

    ./feedback_log run --dates 2020-01-25 2020-01-26 --proxy hahn --scale daily


[dump_feedback_to_yt]: /arc/trunk/arcadia/maps/wikimap/stat/dump_feedback_to_yt
[feedback_table]:      https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db
[social.commit_event]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/social/social_commit_event

[schema]:              /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/libs/schema
