# B2BGeo Tools


### Geocoding tool
https://st.yandex-team.ru/BBGEO-1329

[wiki](https://wiki.yandex-team.ru/b2bgeo/analytics/geocoding-tool/)


### MVRP to Excel tool
https://st.yandex-team.ru/BBGEO-1459


### Billing tool
https://st.yandex-team.ru/BBGEO-1485

[wiki](https://wiki.yandex-team.ru/b2bgeo/analytics/billing-tool/)


### Solver tools
https://st.yandex-team.ru/BBGEO-1996

[wiki](https://wiki.yandex-team.ru/b2bgeo/analytics/replan-tool/)


### Large matrix download tool
```
large-matrix-download -h
usage: large-matrix-download [-h] -i INPUT -o OUTPUT [-m ROUTING_MODE]
                             [-r MATRIX_ROUTER] [-d DATE] [-z TIME_ZONE]
                             [--days DAYS] [-c CHUNK_SIZE] [-j THREADS]

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
  -o OUTPUT, --output OUTPUT
  -m ROUTING_MODE, --routing-mode ROUTING_MODE
  -r MATRIX_ROUTER, --matrix-router MATRIX_ROUTER
  -d DATE, --date DATE
  -z TIME_ZONE, --time-zone TIME_ZONE
  --days DAYS           download matrix for this time of days
  -c CHUNK_SIZE, --chunk-size CHUNK_SIZE
                        split matrix into chunks of this size
  -j THREADS, --threads THREADS
                        download in this number of threads
```