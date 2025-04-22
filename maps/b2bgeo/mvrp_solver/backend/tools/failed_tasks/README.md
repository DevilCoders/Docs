# Failed solver tasks

Utility gets short info about recent vrp tasks with statuses internal_error and lost.

## Local binary run

```
ya make -r bin
./bin/failed_tasks --psql-host `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o hosts_replica_first` --psql-dbname `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_name` --psql-user `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_user` --psql-password `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o password` --offset 1440
```

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-asyncsolver/ci/actions/launches?dir=maps%2Fb2bgeo%2Fmvrp_solver%2Fbackend%2Ftools%2Ffailed_tasks&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/mvrp_solver/backend/tools/failed_tasks
    ```
4. Start release.
    ```
    ya tool sedem release start maps/b2bgeo/mvrp_solver/backend/tools/failed_tasks
    ```
    The command updates corresponding sandbox scheduler [FAILED_SOLVER_TASKS](https://sandbox.yandex-team.ru/scheduler/704375/view).

#### Some hints
* Link to sb-scheduler can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info -v .
    Loading service state.....
    ┌ Sandbox task failed-solver-tasks ──────────────────────┬─────────────────┬────────────────────┬────────────────────────────────────────────────────────────┐
    │                   │ Status                             │ Version         │ St ticket          │ Comment                                                    │
    ├───────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼────────────────────────────────────────────────────────────┤
    │ scheduler_testing │ Deployed (2022-02-22 12:09:52)     │ v1.1 (r9171041) │ MAPSRELEASES-16312 │ (@dtyo) Tool to get short info about recently failed tasks │
    │                   │ https://nda.ya.ru/t/nYv_lvJv4p787n │                 │                    │                                                            │
    └───────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴────────────────────────────────────────────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22b2bgeo-failed-solver-tasks%22%7D)



### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/FAILED_SOLVER_TASKS run --enable-taskbox --type FAILED_SOLVER_TASKS --create-only
```

`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.
