# YCB application tests

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-courier/ci/actions/launches?dir=maps%2Fb2bgeo%2Fya_courier%2Fbackend%2Fapplication_tests&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/ya_courier/backend/application_tests
    ```
4. Start release of **application tests**.
    ```
    ya tool sedem release start maps/b2bgeo/ya_courier/backend/application_tests
    ```
    The command updates corresponding sandbox template for ycb application tests in testing [MAPS_B2BGEO_YCB_APPLICATION_TEST_TEMPLATE_TESTING](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_YCB_APPLICATION_TEST_TEMPLATE_TESTING).

#### Some hints
* Links to sb-templates can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info . -v
    Loading service state....
    ┌ Sandbox task ycb-application-test ────────────────────┬─────────────────┬────────────────────┬──────────────────────────────────┐
    │                  │ Status                             │ Version         │ St ticket          │ Comment                          │
    ├──────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼──────────────────────────────────┤
    │ template_testing │ Deployed (2022-05-20 12:04:41)     │ v1.1 (r9478969) │ MAPSRELEASES-18378 │ (@dtyo) Application test spec... │
    │                  │ https://nda.ya.ru/t/qFs9VBBD56eXVP │                 │                    │                                  │
    └──────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴──────────────────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={%22sedem_service%22:%20%22b2bgeo-ycb-application-test%22})



### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/YCB_APPLICATION_TEST run --enable-taskbox --type YCB_APPLICATION_TEST --create-only
```

`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.

### Results

Execution log of application test binary can be found in `executor.err` file in sandbox log1 directory.
