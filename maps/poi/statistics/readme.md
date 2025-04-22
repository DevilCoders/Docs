Poi Statistics
===

| Key | Value |
| --- | --- |
| Maintainers | [Maps.GeoQuality](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/22543/view |
| Output tables | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/altay& |
| Stat Report | https://stat.yandex-team.ru/Maps.Wiki/Sprav/PoiMetrics |


Project tree
---

| Directory | Description |
| --- | --- |
| [altay](altay) | Contains binaries for metrics calculation. |
| [executor](executor) | Contains binary for metrics aggregation across Stat Report dimensions. |


I want to write my own metric! What should I do?
---

1. Write a binary that calculates metrics for each organization and put it in the [altay directory](altay). Please, use the [orginfo table](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/data/orginfo&) or any subset as a backbone for your calculations. Be sure, that your output table contains only unique columns across all [output tables](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/altay&).
2. Add your new metric to the [config.json](executor/bin/config.json):
    1. `source` is a name of your metric in the [output tables](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/altay&). If your metric is composite use an array to define `source`. 
    2. `agg` is a name of aggregator to use with your metric. All aggregators are declared in the [calculator.py](executor/lib/calculator.py). If there is no suitable one, feel free to add one of the [nile aggregators](https://logos.yandex-team.ru/statbox/nile/tutorial/metrics.html) or write your own (for reference see `BldOrgsSpreadAggregator` and [docs](https://logos.yandex-team.ru/statbox/nile/advanced_tutorial/extending.html#extending-aggregators))!
    3. `agg_args` is a dictionary with arguments that will be passed to a constructor of selected aggregator.
    4. `daily_aggregation` aggregate daily values by week, month, quarter and year in statface report. Only `avg` (default) and `sum` is supported.
    5. `predicate` predicate for nile aggregator. The only available value for now is `nonzero`: aggregate only nonzero metrics values.
    6. `statface` is a dictionary with arguments that define the future field in the Stat Report. [Look here](https://logos.yandex-team.ru/statbox/nile/manual_detailed.html?highlight=statface#nile.api.v1.statface.fields.StatfaceField) to see all acceptable arguments. All [CalculationFields](https://logos.yandex-team.ru/statbox/nile/manual_detailed.html?highlight=statface#nile.api.v1.statface.calculations.CalculationField) also are declared here. Look in [config.json](executor/bin/config.json) for examples.
    7. Commit your changes.
3. Add your new binary to the Sandbox [task](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/poi/PoiMetricsCalculator):
    1. Add new resource to the [resources.py](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/poi/PoiMetricsCalculator/resources.py).
    2. Add a new Sandbox UI field and put reference to it into `altay_executables_id` to the [\_\_init\_\_.py](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/poi/PoiMetricsCalculator/__init__.py).
4. Build your new binary with `YA_MAKE` on Sandbox ([see this](https://sandbox.yandex-team.ru/task/702829025/view) as a reference). Set your binary resource id and update the [config.json](executor/bin/config.json) in the [Sandbox scheduler](https://sandbox.yandex-team.ru/scheduler/22543/view). To upload the new version of [config.json](executor/bin/config.json) use this fancy command `ya upload --ttl=inf --sandbox -T POI_METRICS_EXECUTOR_CONFIG_RESOURCE ./config.json`.
5. Don't forget to click "Save".
