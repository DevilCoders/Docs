# Учим tlm - tape

Команда запуска `./tenfifty_tool ../example_tasks/train_catboost.yaml tape  --yt_work_dir some_dir`

Лог запуска
``` bash
2021-11-06 22:52:23 [INFO] Queued task: root
2021-11-06 22:52:23 [INFO] Starting task: root
2021-11-06 22:52:23 [INFO] Queued task: root -> get_table
2021-11-06 22:52:23 [INFO] Queued task: root -> split_pool
2021-11-06 22:52:23 [INFO] Queued task: root -> prepare_pools -> prepare_pools__test_pool
2021-11-06 22:52:23 [INFO] Queued task: root -> prepare_pools -> prepare_pools__train_pool
2021-11-06 22:52:23 [INFO] Queued task: root -> train_model
2021-11-06 22:52:23 [INFO] Queued task: root -> upload_to_yt
2021-11-06 22:52:23 [INFO] Queued task: root -> apply_model -> apply_model__test_dataset
2021-11-06 22:52:23 [INFO] Queued task: root -> apply_model -> apply_model__train_dataset
2021-11-06 22:52:23 [INFO] root: waiting for subtasks - root -> get_table, root -> split_pool, root -> prepare_pools -> prepare_pools__test_pool, root -> prepare_pools -> prepare_pools__train_pool, root -> train_model, root -> upload_to_yt, root -> apply_model -> apply_model__test_dataset, root -> apply_model -> apply_model__train_dataset
2021-11-06 22:52:24 [INFO] Starting task: root -> get_table
2021-11-06 22:52:26 [INFO] Task root -> get_table finished.  Submitted by root
2021-11-06 22:52:26 [INFO] Starting task: root -> split_pool
Execution is in progress | 10.11 seconds elapsed               2021-11-06 22:52:40 [INFO] Task root -> split_pool finished.  Submitted by root
2021-11-06 22:52:40 [INFO] Starting task: root -> prepare_pools -> prepare_pools__train_pool
2021-11-06 22:52:40 [INFO] Starting task: root -> prepare_pools -> prepare_pools__test_pool
2021-11-06 22:52:40 [INFO] Queued task: root -> prepare_pools -> prepare_pools__train_pool -> format -> train_pool
2021-11-06 22:52:40 [INFO] Queued task: root -> prepare_pools -> prepare_pools__train_pool -> sort -> train_pool
2021-11-06 22:52:40 [INFO] root -> prepare_pools -> prepare_pools__train_pool: waiting for subtasks - root -> prepare_pools -> prepare_pools__train_pool -> format -> train_pool, root -> prepare_pools -> prepare_pools__train_pool -> sort -> train_pool
2021-11-06 22:52:41 [INFO] Queued task: root -> prepare_pools -> prepare_pools__test_pool -> format -> test_pool
2021-11-06 22:52:41 [INFO] Queued task: root -> prepare_pools -> prepare_pools__test_pool -> sort -> test_pool
2021-11-06 22:52:41 [INFO] root -> prepare_pools -> prepare_pools__test_pool: waiting for subtasks - root -> prepare_pools -> prepare_pools__test_pool -> format -> test_pool, root -> prepare_pools -> prepare_pools__test_pool -> sort -> test_pool
2021-11-06 22:52:41 [INFO] Starting task: root -> prepare_pools -> prepare_pools__test_pool -> format -> test_pool
2021-11-06 22:52:41 [INFO] Starting task: root -> prepare_pools -> prepare_pools__train_pool -> format -> train_pool
(3/3) [CACHED] config_dump: 100%|###########################################################################################################################| 646M/646M
(3/3) [CACHED] config_dump: 100%|###########################################################################################################################| 646M/646M
2021-11-06 22:52:48,126 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=fc4fce6d-81ecfae2-3fe03e8-c7acb482&tab=details
2021-11-06 22:52:48,130 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=82a81932-8205c07f-3fe03e8-31bc2be5&tab=details
2021-11-06 22:52:48,227 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5 starting
2021-11-06 22:52:48,264 ( 0 min)    operation fc4fce6d-81ecfae2-3fe03e8-c7acb482 initializing
2021-11-06 22:52:49,471 ( 0 min)    Unrecognized spec: {'mapper': {'title': 'PrepareCatboostPoolRecordForma'}, 'legacy_controller_fraction': 0L}
2021-11-06 22:52:49,471 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5 materializing
2021-11-06 22:52:49,517 ( 0 min)    Unrecognized spec: {'mapper': {'title': 'PrepareCatboostPoolRecordForma'}, 'legacy_controller_fraction': 0L}
2021-11-06 22:52:49,518 ( 0 min)    operation fc4fce6d-81ecfae2-3fe03e8-c7acb482 materializing
2021-11-06 22:53:04,509 ( 0 min)    operation fc4fce6d-81ecfae2-3fe03e8-c7acb482: running=1     completed=0     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:04,610 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5: running=0     completed=0     pending=1     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:06,154 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5: running=1     completed=0     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:17,274 ( 0 min)    operation fc4fce6d-81ecfae2-3fe03e8-c7acb482 completing
2021-11-06 22:53:18,879 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5 completing
2021-11-06 22:53:19,960 ( 0 min)    operation fc4fce6d-81ecfae2-3fe03e8-c7acb482 completed
2021-11-06 22:53:20 [INFO] Task root -> prepare_pools -> prepare_pools__train_pool -> format -> train_pool finished.  Submitted by root -> prepare_pools -> prepare_pools__train_pool
2021-11-06 22:53:20 [INFO] Starting task: root -> prepare_pools -> prepare_pools__train_pool -> sort -> train_pool
2021-11-06 22:53:21,077 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=2d006e28-f8bbf1a-3fe03e8-a67e36ff&tab=details
2021-11-06 22:53:21,170 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff initializing
2021-11-06 22:53:21,575 ( 0 min)    operation 82a81932-8205c07f-3fe03e8-31bc2be5 completed
2021-11-06 22:53:22,375 ( 0 min)    Unrecognized spec: {'legacy_controller_fraction': 0L}
2021-11-06 22:53:22,376 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff materializing
2021-11-06 22:53:22 [INFO] Task root -> prepare_pools -> prepare_pools__test_pool -> format -> test_pool finished.  Submitted by root -> prepare_pools -> prepare_pools__test_pool
2021-11-06 22:53:22 [INFO] Starting task: root -> prepare_pools -> prepare_pools__test_pool -> sort -> test_pool
2021-11-06 22:53:23,025 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=d3c942c1-1c36c67e-3fe03e8-b33535d3&tab=details
2021-11-06 22:53:23,111 ( 0 min)    operation d3c942c1-1c36c67e-3fe03e8-b33535d3 initializing
2021-11-06 22:53:24,303 ( 0 min)    Unrecognized spec: {'legacy_controller_fraction': 0L}
2021-11-06 22:53:24,303 ( 0 min)    operation d3c942c1-1c36c67e-3fe03e8-b33535d3 materializing
2021-11-06 22:53:34,871 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff: running=0     completed=0     pending=1     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:35,384 ( 0 min)    operation d3c942c1-1c36c67e-3fe03e8-b33535d3: running=0     completed=0     pending=1     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:37,793 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff: running=1     completed=0     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:39,604 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff completing
2021-11-06 22:53:39,697 ( 0 min)    operation d3c942c1-1c36c67e-3fe03e8-b33535d3: running=0     completed=1     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 22:53:41,255 ( 0 min)    operation d3c942c1-1c36c67e-3fe03e8-b33535d3 completed
2021-11-06 22:53:41,286 ( 0 min)    operation 2d006e28-f8bbf1a-3fe03e8-a67e36ff completed
2021-11-06 22:53:42 [INFO] Task root -> prepare_pools -> prepare_pools__train_pool -> sort -> train_pool finished.  Submitted by root -> prepare_pools -> prepare_pools__train_pool
2021-11-06 22:53:42 [INFO] Task root -> prepare_pools -> prepare_pools__test_pool -> sort -> test_pool finished.  Submitted by root -> prepare_pools -> prepare_pools__test_pool
2021-11-06 22:53:42 [INFO] root -> prepare_pools -> prepare_pools__test_pool is awake
2021-11-06 22:53:42 [INFO] root -> prepare_pools -> prepare_pools__train_pool is awake
[UPLOAD]: 186: 100%|#################################################################################################################| 44.0/44.0 [00:00<00:00, 258iB/s2021-11-06 22:53:44 [INFO] Task root -> prepare_pools -> prepare_pools__train_pool finished.  Submitted by root
2021-11-06 22:53:45 [INFO] Task root -> prepare_pools -> prepare_pools__test_pool finished.  Submitted by root
2021-11-06 22:53:45 [INFO] Starting task: root -> train_model
INFO: Nirvana workflow created

    https://nirvana.yandex-team.ru/flow/aa502fab-7652-422c-af1c-85f805350e3d/2348fc22-f442-48ef-80d1-a4bbf103de78

API: startWorkflow

API: startWorkflow  --->  OK

2021-11-06 23:00:57 [INFO] Task root -> train_model finished.  Submitted by root
2021-11-06 23:00:57 [INFO] Starting task: root -> apply_model -> apply_model__train_dataset
2021-11-06 23:00:57 [INFO] Starting task: root -> apply_model -> apply_model__test_dataset
2021-11-06 23:00:58 [INFO] Starting task: root -> upload_to_yt
2021-11-06 23:00:59 [INFO] Task root -> upload_to_yt finished.  Submitted by root
2021-11-06 23:00:59 [INFO] Queued task: root -> apply_model -> apply_model__test_dataset -> apply_catboost -> test_dataset
2021-11-06 23:00:59 [INFO] root -> apply_model -> apply_model__test_dataset: waiting for subtasks - root -> apply_model -> apply_model__test_dataset -> apply_catboost -> test_dataset
2021-11-06 23:00:59 [INFO] Queued task: root -> apply_model -> apply_model__train_dataset -> apply_catboost -> train_dataset
2021-11-06 23:00:59 [INFO] root -> apply_model -> apply_model__train_dataset: waiting for subtasks - root -> apply_model -> apply_model__train_dataset -> apply_catboost -> train_dataset
2021-11-06 23:01:00 [INFO] Starting task: root -> apply_model -> apply_model__train_dataset -> apply_catboost -> train_dataset
2021-11-06 23:01:00 [INFO] Starting task: root -> apply_model -> apply_model__test_dataset -> apply_catboost -> test_dataset
(3/3) [CACHED] config_dump: 100%|###########################################################################################################################| 646M/646M
(3/3) [CACHED] config_dump: 100%|###########################################################################################################################| 646M/646M
2021-11-06 23:01:06,609uINFO100%Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=faf93ffd-bbae8a26-3fe03e8-5c381b65&tab=details##| 646M/646M
2021-11-06 23:01:06,617 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=2a9afe-336da32-3fe03e8-17c426ee&tab=details
2021-11-06 23:01:06,696 ( 0 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65 starting
2021-11-06 23:01:06,696 INFO    operation 2a9afe-336da32-3fe03e8-17c426ee starting
2021-11-06 23:01:07,932 ( 0 min)    Unrecognized spec: {'mapper': {'title': 'ApplyCatboostModelMapper'}, 'legacy_controller_fraction': 0L}
2021-11-06 23:01:07,932 ( 0 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65 materializing
2021-11-06 23:01:07,947 ( 0 min)    Unrecognized spec: {'mapper': {'title': 'ApplyCatboostModelMapper'}, 'legacy_controller_fraction': 0L}
2021-11-06 23:01:07,947 ( 0 min)    operation 2a9afe-336da32-3fe03e8-17c426ee materializing
2021-11-06 23:01:19,222 ( 0 min)    operation 2a9afe-336da32-3fe03e8-17c426ee: running=0     completed=0     pending=1     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 23:01:19,379 ( 0 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65: running=1     completed=0     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 23:01:20,647 ( 0 min)    operation 2a9afe-336da32-3fe03e8-17c426ee: running=1     completed=0     pending=0     failed=0     aborted=0     lost=0     total=1     blocked=0
2021-11-06 23:02:19,778 ( 1 min)    operation 2a9afe-336da32-3fe03e8-17c426ee completing
2021-11-06 23:02:24,901 ( 1 min)    operation 2a9afe-336da32-3fe03e8-17c426ee completed
2021-11-06 23:02:29 [INFO] Task root -> apply_model -> apply_model__test_dataset -> apply_catboost -> test_dataset finished.  Submitted by root -> apply_model -> apply_model__test_dataset
2021-11-06 23:02:29 [INFO] root -> apply_model -> apply_model__test_dataset is awake
2021-11-06 23:02:30 [INFO] Task root -> apply_model -> apply_model__test_dataset finished.  Submitted by root
2021-11-06 23:02:45,239 ( 1 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65: running=1     completed=1     pending=0     failed=0     aborted=0     lost=0     total=2     blocked=0
2021-11-06 23:03:00,781 ( 1 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65 completing
2021-11-06 23:03:05,878 ( 1 min)    operation faf93ffd-bbae8a26-3fe03e8-5c381b65 completed
2021-11-06 23:03:07 [INFO] Task root -> apply_model -> apply_model__train_dataset -> apply_catboost -> train_dataset finished.  Submitted by root -> apply_model -> apply_model__train_dataset
2021-11-06 23:03:07 [INFO] root -> apply_model -> apply_model__train_dataset is awake
2021-11-06 23:03:08 [INFO] Task root -> apply_model -> apply_model__train_dataset finished.  Submitted by root
2021-11-06 23:03:08 [INFO] root is awake
2021-11-06 23:03:09 [INFO] Task root finished.
```
