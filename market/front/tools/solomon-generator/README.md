## solomon-generator

PoC уноса графиков и дашборд в код.

[пример сгенерённой дашборды (need for speed)](https://solomon.yandex-team.ru/?project=market-front&cluster=production&period=one_hour&service=market_front_desktop&quantile=0.95&dashboard=need-for-speed)


Для добавления новых дашборды заводим новые файлы в dashboards, для общих меджу ними графиков — в graphs
если надо попрограммировать — пишем код в templates

Как раскатить:
```
ya make
export SOLOMON_API_KEY=AQAD-yOUR-SoloMon-OaUTH-Key
./solomon-generator
```
