# VIMOBU

vimobu = Viewed Models By User
Отдает просмотренные модели по yandexuid.
Изначальная задача: https://st.yandex-team.ru/MARKETOUT-17519

Робот для доступа в YT: https://staff.yandex-team.ru/robot-market-vimobu

Ходит в таблицу которую пишут маркетные рекомендации: //home/market/prestable/yamarec/rt-logger/we_have_cheaper
1. https://yt.yandex-team.ru/zeno/#page=navigation&path=//home/market/prestable/yamarec/rt-logger/we_have_cheaper&offsetMode=key

## production
1. <http://vimobu.vs.market.yandex.net:29335/ping>

## testing
1. <http://vimobu.tst.vs.market.yandex.net:29335/ping>

## development
```
./run --port 2606
```

### Deploy
1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_VIEWED_MODELS_BY_USER_APP {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"


## API

### /ping

### /select
1. ```/select/{yandex_uid}```
2. ```/select/{yandex_uid}/{count}```
3. ```/select/yandexuid:{yandex_uid}```
Пример:
<pre>
```
manushkin@laptop:~$ curl -s localhost:2606/select/689089771449002886
[
  1816483305, 
  1724711179, 
  1732036564
]
manushkin@laptop:~$ curl -s localhost:2606/select/689089771449002886/1
[
  1816483305
]
```
</pre>
