# Stress tests

## Generating ammo

1. Get requests to v1 from YQL in JSON format: https://yql.yandex-team.ru/Queries/5ac00d9222e2e73e0bcb7eac

```sql
PRAGMA yt.Pool = "MAPSAPI";

SELECT
    request,
    ip
FROM hahn.`home/logfeller/logs/maps-front-production-log/1d/2019-08-14`
WHERE tskv_format = 'front-search-service_app'
    AND request LIKE '/services/search/v1%'
    AND status LIKE '200'
LIMIT 2000000;
```

2. Build project

```sh
make build
```

3. Generate ammo:

```
node ./out/src/tests/stress/gen-ammo.js < <path-to-yql-data> > ammo.txt
```

4. Upload resulting ammo to MDS and update URLs in shooting configurations.
