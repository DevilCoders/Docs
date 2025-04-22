# Сервис подбора вариантов поездки выходного дня.

https://st.yandex-team.ru/TRAVELMARKETING-68

## Локальный запуск
1. Нужна postgresql база, используется только на чтение, поэтому можно использовать [тестовую weekendtour](https://yc.yandex-team.ru/folders/foo1262pmfvsq72flh90/managed-postgresql/cluster/mdb9sssbmtcje8gtvlrc?section=databases)
1. `cp ./config/weekendtour.samples/config.development.yaml ./config/weekendtour/`
1. `vim ./config/weekendtour/config.development.yaml`
1. `./tools/run_dev.sh`
1. `grpcurl -v -emit-defaults -plaintext localhost:9001 list`
1. `curl "http://localhost:9000/ping"`
1. `curl "http://localhost:9000/weekend-tours?weekendId=20210702"`

В параметре weekendId нужно указывать пятницу интересующих выходных (в примере - второе июля).
