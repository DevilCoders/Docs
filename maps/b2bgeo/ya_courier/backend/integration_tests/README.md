# YCB integration tests

## Local binary run

```
ya make -r bin
./bin/ya_courier_integration_test
```

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-courier/ci/actions/launches?dir=maps%2Fb2bgeo%2Fya_courier%2Fbackend%2Fintegration_tests&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/ya_courier/backend/integration_tests
    ```
4. Start release of **integration tests**.
    ```
    ya tool sedem release start maps/b2bgeo/ya_courier/backend/integration_tests
    ```
    The command updates corresponding sandbox template for ycb integration tests in testing [MAPS_B2BGEO_YCB_INTEGRATION_TEST_TEMPLATE_TESTING](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_YCB_INTEGRATION_TEST_TEMPLATE_TESTING).

#### Some hints
* Links to sb-templates can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info . --verbose
    Loading service state....
    ┌ Sandbox task ycb-integration-test ────────────────────┬─────────────────┬────────────────────┬──────────────────────────────────────────────────┐
    │                  │ Status                             │ Version         │ St ticket          │ Comment                                          │
    ├──────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼──────────────────────────────────────────────────┤
    │ template_testing │ Deployed (2022-05-19 14:13:26)     │ v1.1 (r9474386) │ MAPSRELEASES-18333 │ (@dtyo) ycb integration tests under sedem_config │
    │                  │ https://nda.ya.ru/t/pk3GHyxq56YTQj │                 │                    │                                                  │
    └──────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴──────────────────────────────────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22b2bgeo-ycb-integration-test%22%7D)



### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/YCB_INTEGRATION_TEST run --enable-taskbox --type YCB_INTEGRATION_TEST --create-only
```

`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.

### Results

Execution log of integration test binary can be found in `executor.err` file in sandbox log1 directory.
