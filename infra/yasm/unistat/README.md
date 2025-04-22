TODO
====
 * remove hacks
 * support for push
 * better api
 * move to library/python/unistat

Example:
========
```
import json

from infra.yasm.unistat import global_unistat, AggregationType, SuffixType

some_metric = global_unistat.create_float(
    name='signal_name',
    tags=[('prj', 'something')],
    suffix=SuffixType.Sum,
    aggregation_type=AggregationType.Sum
)
some_metric.push(1.0)

# [['prj=something;signal_name_summ', 1]]
print(json.loads(global_unistat.to_json()))
```
