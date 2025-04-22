# Pipedrive Gate integration tests



## Local binary run

### Testing pipedrive-gate that runs in QLoud test environment

    ya make -r bin; PIPEDRIVE_API_TOKEN=$(ya vault get version `ya vault list secrets | grep pipedrive_test | awk '{print $2}'` -o api_token) ./bin/pipedrive_gate_integration_test

### Testing pipedrive-gate that runs locally

Execute in the ../bin directory:

    ya make -r ../bin; PIPEDRIVE_DOMAIN=b2bgeo-sandbox PIPEDRIVE_API_TOKEN=$(ya vault get version `ya vault list secrets | grep pipedrive_test | awk '{print $2}'` -o api_token) ../bin/pipedrive_gate

Then, execute in ./bin directory:

    ya make -r ; PIPEDRIVE_GATE_URLS=http://127.0.0.1:5555 PIPEDRIVE_API_TOKEN=$(ya vault get version `ya vault list secrets | grep pipedrive_test | awk '{print $2}'` -o api_token) ./bin/pipedrive_gate_integration_test

## Sandbox task

### Release process
1. Commit changes to arcadia.
2. Wait until auto build is done ([Action in CI](https://a.yandex-team.ru/projects/maps-b2bgeo-pipedrive-gate/ci/actions/launches?dir=maps%2Fb2bgeo%2Fpipedrive_gate%2Fintegration_tests&id=build)).
3. Check that sedem has new release candidate (here and after all sedem commands are the same as for Nanny services).
    ```
    ya tool sedem release info maps/b2bgeo/pipedrive_gate/integration_tests
    ```
4. Start release of **integration tests**.
    ```
    ya tool sedem release start maps/b2bgeo/pipedrive_gate/integration_tests
    ```
    The command updates corresponding sandbox template for pipedrive-gate integration tests in testing [MAPS_B2BGEO_PIPRDRIVE_GATE_INTEGRATION_TEST_TEMPLATE_TESTING](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_PIPRDRIVE_GATE_INTEGRATION_TEST_TEMPLATE_TESTING).

#### Some hints
* Links to sb-templates can easily be found using `sedem info` with `-v`:
    ```
    $ ya tool sedem release info . -v
    Loading service state....
    ┌ Sandbox task piprdrive-gate-integration-test ─────────┬─────────────────┬────────────────────┬──────────────────────────────────┐
    │                  │ Status                             │ Version         │ St ticket          │ Comment                          │
    ├──────────────────┼────────────────────────────────────┼─────────────────┼────────────────────┼──────────────────────────────────┤
    │ template_testing │ Deployed (2022-05-19 17:36:38)     │ v1.1 (r9475992) │ MAPSRELEASES-18366 │ (@dtyo) BBGEO-13458: config c... │
    │                  │ https://nda.ya.ru/t/HY7uCZD_56ZT5r │                 │                    │                                  │
    └──────────────────┴────────────────────────────────────┴─────────────────┴────────────────────┴──────────────────────────────────┘
    ```
    nda.ya.ru link in Status field is what you need.

* Sedem service page is [here](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={%22sedem_service%22:%20%22b2bgeo-piprdrive-gate-integration-test%22})



### Build and run
Command below creates draft of sandbox task and prints its url.

```
ya make -r task/
./task/PIPEDRIVE_GATE_INTEGRATION_TEST run --enable-taskbox --type PIPEDRIVE_GATE_INTEGRATION_TEST --create-only
```

`--enable-taskbox` is required, otherwise sandbox will try to find the task in `sandbox/projects`.

### Results

Execution log of integration test binary can be found in `executor.err` file in sandbox log1 directory.
