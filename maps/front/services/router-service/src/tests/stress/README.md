# Stress tests

## Generating ammo

1. Select requests from access logs in [YQL](https://yql.yandex-team.ru/):

    ```sql
    PRAGMA yt.Pool = 'MAPSAPI';

    SELECT
        request,
        x_real_ip,
        referer
    FROM hahn.`logs/geo-access-log/1d/2019-07-01` -- specify needed date
    WHERE
        vhost = 'api-maps.yandex.ru'
        AND (
            request LIKE '/services/route/v2%'
            OR request LIKE '/services/route/2.0%'
        );
    ```

    Then download result in `JSON` format.

2. Generate ammo from `YQL` data:

    ```sh
    make build
    node out/tests/stress/generate-ammo.js < path-to-yql-data > ammo.txt
    ```

3. Load ammo to `MDS`:

    ```sh
    gzip -c -9 ammo.txt > ammo.txt.gz
    curl https://lunapark.yandex-team.ru/api/addammo.json -F'login=<your_login>' -F'dsc=<description>' -F'file=@ammo.txt.gz'
    ```

    Then update `phantom.ammofile` in [capacity.yaml](capacity.yaml) configuration to URL from
    response.
