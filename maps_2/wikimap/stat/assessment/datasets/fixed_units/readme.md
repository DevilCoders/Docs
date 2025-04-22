Fixed Units Dataset
===================
Generates [//home/maps/core/nmaps/analytics/assessment/datasets/fixed\_units\_dataset][fixed_units_dataset] tables. Tables contain
stats on fixes of incorrect units intended for datalens dashboard/dataset.

Relies on [assessment\_unit\_table][assessment_unit_table] replica and [puid\_info][puid_info] dictionaries on Hahn cluster.

Usage
-----
This tool is a _nile cli udf_ with the following required parameters:
* `--dates <dates>` - dates (YYYY-MM-DD);
* `--recalc-prior-days <n_days>` - also calculate `n_days` prior dates for each `date` (optional, default: 28 + 7 - 1);
* `--proxy <cluster>` - cluster where calculations must be run;
* `--scale <scale>` - required by the RJM framework. Expected to be `daily` in this tool;
* `--use-yql` - yql backend should be used.

Usage example:

    ya nile ./udf/libassessment_fixed_units_dataset.so -- run --proxy hahn --scale daily --dates <dates> --use-yql


[puid_info]: http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/puid_info
[assessment_unit_table]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-nmaps/analytics/tasks_payment/replica/assessment_nmaps-14585/assessment_unit
[fixed_units_dataset]:   http://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/assessment/datasets/fixed_units
