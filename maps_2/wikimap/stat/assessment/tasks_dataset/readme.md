Tasks Dataset
=============
Generates [//home/maps/core/nmaps/analytics/assessment/datasets/tasks][tasks_dataset] tables. Tables contain tasks assessment stats over multiple dimensions (such as region or tariff) intended for datalens dashboard/dataset.

Relies on `tasks_log` and `graded_units_log` from [//home/maps/core/nmaps/analytics/assessment][assessment_logs] on Hahn cluster. Therefore, `graded_units_log` limitation stands: any grade that is 28+ days younger than unit could be ignored.

Usage
-----
This tool is a _nile cli udf_ with the following required parameters:
* `--dates <dates>` - dates (YYYY-MM-DD);
* `--recalc-prior-days <n_days>` - also calculate `n_days` prior dates for each `date` (optional, default: 27);
* `--proxy <cluster>` - cluster where calculations must be run;
* `--scale <scale>` - required by the RJM framework. Expected to be `daily` in this tool;
* `--use-yql` - yql backend should be used.

Usage example:

    ya nile ./udf/libassessment_tasks_dataset.so -- run --proxy hahn --scale daily --dates <dates> --use-yql


[assessment_logs]: http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/assessment
[tasks_dataset]:   http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/assessment/datasets/tasks
