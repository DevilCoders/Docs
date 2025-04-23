Graded Units Log
================
Log contains graded units with `action_at::date` matching log date. Units are extended with region\_id, task\_id, summary grade value and certainty.

Any grade that is 28+ days younger than unit might be ignored.

Relies on replica of `assessment.unit` and `assessment.grade` tables on Hahn cluster [//home/maps/core/nmaps/dynamic/replica/assessment][replica].


Determining summary grade value
-------------------------------
1. If there're any `expert` grades, last expert grade value is used with `certainty=expert`;
2. otherwise, if there's only a single `basic` grade, its value is used with `certainty=basic_single`;
3. otherwise, if there're multiple and unanimous `basic` grades, their value is used with `certainty=basic_unanimosly`;
4. otherwise. if there're multiple `basic` grades with majoriry consensus, this consensus is used with `certainty=basic_majority`;
5. otherwise, if there're any `arbitrary` (i.e. outside-of-sample grades), last arbitrary grade value is with with `certainty=arbitrary`.

Usage
-----
This tool is a _nile cli udf_ with the following required parameters:
* `--dates <date>` - _dates of launch_ (YYYY-MM-DD) to be converted into log dates;
* `--recalc-prior-days <n_days>` - also calculate `n_days` prior dates for each `date` (optional, default: 27);
* `--proxy <cluster>` - cluster where calculations must be run;
* `--scale <scale>` - required by the RJM framework. Expected to be `daily` in this tool;
* `--use-yql` - yql backend should be used.

Usage example:

    ya nile ./udf/libassessment_graded_units_log.so -- run --proxy hahn --scale daily --dates <dates> --use-yql


[replica]: http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/assessment
[grades_log]: http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/assessment/grades_log
