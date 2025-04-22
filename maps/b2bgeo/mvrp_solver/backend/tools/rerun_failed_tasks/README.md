# Rerun failed solver tasks

Utility gets last failed solver task, reruns them and checks the statuses.

## Local binary run

```
ya make -r bin
./bin/rerun_failed_tasks --psql-env-secret sec-01ddnqwb7gjh51xjnskedf8yxc --psql-env-secret sec-01ddnqwd67km3bkn6vyazge0p5 --apikey `ya vault get version sec-01ddqvwahhm3ys13nbyxxq55kr -o apikey` --offset 100 --max-tasks 100 --min-tasks 10 --dry-run
```

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-asyncsolver/ci/actions/launches?dir=maps%2Fb2bgeo%2Fmvrp_solver%2Fbackend%2Ftools%2Frerun_failed_tasks&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/mvrp_solver/backend/tools/rerun_failed_tasks
    ```
4. Start release.
    ```
    ya tool sedem release start maps/b2bgeo/mvrp_solver/backend/tools/rerun_failed_tasks
    ```
    The command updates corresponding [sandbox template](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_RERUN_FAILED_TASKS_TESTING_TEMPLATE/view).

#### Some hints
* Link to sb-scheduler can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info -v .
    Loading service state.....
    ┌ Sandbox task rerun-failed-tasks ───────────────────────┬─────────────────┬────────────────────┬──────────────────────────────┐
    │                   │ Status                             │ Version         │ St ticket          │ Comment                      │
    ├───────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼──────────────────────────────┤
    │ testing_template  │ Deployed (2022-03-25 10:42:55)     │ v1.1 (r9271424) │ MAPSRELEASES-17077 │ (@gorokhov) BBGEO-13301: ... │
    │                   │ https://nda.ya.ru/t/uq_ZJQ114sntKF │                 │                    │                              │
    └───────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴──────────────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22b2bgeo-rerun-failed-tasks%22%7D)


### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/B2BGEO_RERUN_FAILED_TASKS run --enable-taskbox --type B2BGEO_RERUN_FAILED_TASKS --create-only
```
`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.
