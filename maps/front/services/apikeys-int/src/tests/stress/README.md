# Stress tests

## Generating ammo

1. Select requests from access logs in [YQL](https://yql.yandex-team.ru/):

    ```sql
    SELECT
        String::UnescapeC(Yson::ConvertToString(Yson::Lookup(Yson::Parse(_rest), "request_body"))) as request_body
    FROM
        hahn.`home/logfeller/logs/maps-front-production-log/1d/2022-03-10`
    WHERE
        tskv_format = 'maps-front-apikeys-int_app'
        AND request = "/v1/check"
    LIMIT 50000
    ```

    Then download *full result* in `TSV` format.

2. Generate ammo from `YQL` data:

    ```sh
    make build
    node out/tests/stress/generate-ammo.js < path-to-yql-data > ammo.txt
    ```

3. Load ammo to `MDS`:

    ```sh
    curl https://lunapark.yandex-team.ru/api/addammo.json -F'login=<your_login>' -F'dsc=<description>' -F'file=@ammo.txt'
    ```

    Then update `phantom.ammofile` in [capacity.yaml](capacity.yaml) configuration to URL from
    response.

## TVM

Because `Y.Deploy` cannot start `TVM` daemon in `unittest` mode, start `TVM` daemon locally for
`stress` environment.

* Original ticket about this issue in `Qloud`: https://st.yandex-team.ru/QLOUDDEV-2356
* Ticket about `unittest` support in `Y.Deploy`: https://st.yandex-team.ru/DEPLOY-1097
