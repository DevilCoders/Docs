The tool generates driving_arrival_points (DAP) snippets for the geo search.
It also provides a set of utilities for geocoding, search and saas-kv access.

Sandbox schedulers:
* [Testing](https://sandbox.yandex-team.ru/scheduler/20045/view)
* [Production](https://sandbox.yandex-team.ru/scheduler/11528/view)

Main scenarios are listed below.

A. Steps to generate snippets for TaskManager (https://wiki.yandex-team.ru/users/karas-pv/SnippetsTaskManager/):

1\) Generate 'all' snippets table (organization and toponyms are together).
(filter out far clusters - clusters with distance_to_target bigger than 750 meters)
```
dap_snippets --generate //path_to_mined_table -o //output_folder
```

2\) Filter errors and duplicate snippet keys.
```
dap_snippets --filter-errors //all_snippets_table -o //all_filtered_table
```
3\) Merge snippets from different sources (Nyak export, Sprav).
```
dap_snippets -m //all_filtered_table --nyak //nyak_export_table --sprav /path_to_sprav_company_export -o //all_patched_table
```
4\) Split 'all' table in 'organizations' and 'toponyms' as TaskManager needs them separately.
```
dap_snippets -s //all_patched_table -o //ready_snippets_folder
```
