## Python-интерфейс к ymod_unistat


```
import py_unistat
import json

unistat = py_unistat.find_module("unistat_mod_name")

if unistat:
    unistat.is_metric_present("m1")
    unistat.add_metric(json.dumps({name : "m1", aggregate: "...", ...}))
    unistat.push("m1", 0.1)
    values = json.loads(unistat.get_values_in_json_str)

```
