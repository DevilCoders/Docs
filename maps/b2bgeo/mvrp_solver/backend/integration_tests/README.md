# Solver integration tests

## Local binary run

```
ya make -r bin
./bin/solver_integration_test
```

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-asyncsolver/ci/actions/launches?dir=maps%2Fb2bgeo%2Fmvrp_solver%2Fbackend%2Fintegration_tests&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/mvrp_solver/backend/integration_tests
    ```
4. Start release of **integration tests**.
    ```
    ya tool sedem release start maps/b2bgeo/mvrp_solver/backend/integration_tests
    ```
    The command updates corresponding sandbox template for solver integration tests in testing [MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_TESTING](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_TESTING/view).
5. Start corresponding release of **solver** to testing. New version of acceptance integration tests will run for testing.
6. Step corresponding release of **solver** to prestable. No tests will run.
7. Step release of **integration tests** to stable.
    ```
    ya tool sedem release step maps/b2bgeo/mvrp_solver/backend/integration_tests 1.1 stable
    ```
    The command updates corresponding sandbox template for solver integration tests in stable [MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_STABLE](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_STABLE)
8. Step release of **solver** to stable. New version of acceptance integration tests will run for stable.

#### Some hints
* Links to sb-templates can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info -v .
    Loading service state......
    ┌ Sandbox task solver-integration-test ─────────────────┬─────────────────┬────────────────────┬────────────────────┐
    │                  │ Status                             │ Version         │ St ticket          │ Comment            │
    ├──────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼────────────────────┤
    │  template_stable │ Deployed (2022-01-24 13:32:04)     │ v1.1 (r9059583) │ MAPSRELEASES-15478 │ (@dtyo) fix a.yaml │
    │                  │ https://nda.ya.ru/t/R7He7lPF4kjMti │                 │                    │                    │
    ├──────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼────────────────────┤
    │ template_testing │ Deployed (2022-01-21 22:19:35)     │ v1.1 (r9059583) │ MAPSRELEASES-15478 │ (@dtyo) fix a.yaml │
    │                  │ https://nda.ya.ru/t/lqWX6xe54kj5oD │                 │                    │                    │
    └──────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22b2bgeo-solver-integration-test%22%7D)



### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/SOLVER_INTEGRATION_TEST run --enable-taskbox --type SOLVER_INTEGRATION_TEST --create-only
```

`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.

### Results

Execution log of integration test binary can be found in `executor.err` file in sandbox log1 directory.
