# Stress tests for search-api

## Generating ammo

1. Get requests to v1 from YQL in TSKV format: https://yql.yandex-team.ru/Operations/XWGWjDa9vHONpmuViHuv32yv50fDydUKPFo8mspVe7c=
2. Save it to `src/tests/stress/search/v1/yt.log`.
3. Generate ammo and upload it to MDS:
```
./generate-search-ammo.sh
```
