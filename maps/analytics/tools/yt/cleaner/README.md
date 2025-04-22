# YT cleaner

Утилита для чистки таблиц на YT

Так как нет стандартного `TTL` в самом `YT` (есть только YQL, но он не совместим с указанием транзакции)


## How to run
```bash
ya make
./bin --path //home/maps/analytics/tmp/r-kucherov --ttl-days 7 -f
```