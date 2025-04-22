### TK calls count by day
From `tk_calls` table.

Usage: ```./count_by_day.sh from_dt to_dt```

Prefer dates in ISO-8601 date format.

Result structure:
* `date` - date from `script_started` column
* `input_calls` - count of input calls (`direction = 1`) by day
* `output_calls` - count of output calls (`direction = 2`) by day
* `other_calls` - count of other calls. have to be 0. for debug.
* `all_calls` - full count of calls

For example:
```bash
$ ./bin/count_by_day.sh 2018-01-01 2018-09-19
$ cat tmp/count_by_day.2018-01-01_2018-09-19.tsv
date        input_calls  output_calls  other_calls  all_calls
2018-08-28  0            0             1            1
2018-09-05  373          0             0            373
...
```