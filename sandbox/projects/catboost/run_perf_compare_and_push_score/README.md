# Speed bench
There are two very similar SandBox tasks for benchmarking CatBoost.
The first task benchmarks a single CatBoost executable file specified by either a SandBox resource ID, or by the SVN revision to build CatBoost from.
The second task benchmarks and compares two CatBoost executable files.
You may find the second task here, **RUN_CAT_BOOST_PERF_COMPARE_AND_PUSH_SCORE** ([task example](https://sandbox.yandex-team.ru/task/325210708/view)).

The task has following input parameters:
- `use last binary archive` and `Binary release type` - needed for debugging of the task; do not touch them
- `use first catboost binary` - How to get the first CatBoost executable file -- SandBox resource ID, or SVN revision
    - `first catboost binary` - SandBox resource ID of type **CAT_BOOST_BINARY**; to create, do ```ya upload <binary_path> --type CAT_BOOST_BINARY``` -- see [wiki](https://wiki.yandex-team.ru/yatool/upload/) for more information
    - `first revision number` - SVN revision number to build CatBoost executable file from
- `first catboost binary name` - Name of the first CatBoost executable file for graphs and tables
- `use second catboost binary` - How to get the second CatBoost executable file -- SandBox resource ID, or SVN revision
- `second catboost binary name` - Name of the second CatBoost executable file for graphs and tables
- `push result to yt table` - If True, the result is added to a given YT table
    - `time table proxy` - YT proxy, e.g. `hahn.yt.yandex.net`
    - `time table path` - Path to the YT table, e.g. `//home/mltools/perf_stand/perf_stand_data_table`
    - `create time table` - If True, create the YT table having a strict schema
    - `token name` - YT token SandBox Vault
- `json task` - SandBox resource ID of type **CAT_BOOST_PERF_TEST_JSON_TASK**; see [task example](https://sandbox.yandex-team.ru/resource/686502312/view) for an example; datasets need to be archived and uploaded with type **CAT_BOOST_POOL_ARCHIVE**
- `number of runs` - How many times to benchmark a dataset
- `required fraction of successful tasks` - How many tasks must succeed

## In result
For each dataset, the CatBoost execution time is added to the specified YT table.
TODO(yazevnul): reword `The resources in which the time will also be recorded. You can also see graphs for these runs. They are in resources **RUN_CAT_BOOST_PERF_TEST_ON_TWO_BINARIES** tasks.`

## For creating your tasks
|dataset name               |sandbox resource id|
| ------------------------- | ----------------- |
| higgs                     | 686499343         |
| epsilon                   | 686528822         |
| msrank                    | 686538969         |
| kdd98                     | 686545720         |
| fml_search_pool_big       | 686557239         |
| airlines                  | 686563313         |
| airlines_onehot_small     | 697380179         |
| synthetic-5k-features     | 720155327         |
| synthetic                 | 720210277         |
| abalone                   | 720288777         |
| ad_clicks_small(pairs)    | 720308571         |

