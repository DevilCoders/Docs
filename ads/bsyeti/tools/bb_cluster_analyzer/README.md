# Анализатор состояния кластеров buzzard, resharder, caesar, caesar_worker

На примерах:

```
$ ./bb_cluster_analyzer buzzard discover_shard 10
bootstrap-buzzard2-808.sas.yp-c.yandex.net
```

```
$ ./bb_cluster_analyzer caesar slow_shards --input BannersSystem --stand dev --contour 7
shard  message_lag host lag_details: pythia://home/bigb_resharder_test/caesar/7/EventsQueues/BannerIDSwift,pythia://home/bigb_resharder_test/caesar/7/EventsQueues/BannerID
22     1478          bootstrap-caesar7-4.vla.yp-c.yandex.net/Banners 0,1478
12      814         bootstrap-caesar7-15.sas.yp-c.yandex.net/Banners  0,814
24      626          bootstrap-caesar7-4.vla.yp-c.yandex.net/Banners  0,626
```

Для получения информации о хосте где обрабатывается шард нужно указать топик.
А точнее путь к consuming system читающей этот топик
(обычно систему называют как и топик, но с заменой плохих символов на `_`).
Тулза знает, где на ыте лежат consuming system-ы, но не знает какую систему вы хотите.
Поэтому ей надо указать, последнюю часть пути через `--input`.
Для удобства можно делать это через регулярку.
Если регулярка не однозначно задает систему, будет ошибка с перечислением подходящих систем.

```
$ ./bb_cluster_analyzer resharder discover_shard 10 --input .*iva.*watch.*
bootstrap-resharder-51.iva.yp-c.yandex.net
```


```
$ ./bb_cluster_analyzer caesar_resharder discover_shard 10
__main__.py[LINE:207]# ERROR    [2021-09-10 13:29:34,469]  --input is required for service 'caesar_resharder'. Use '--input .*'
Traceback (most recent call last):
  ....
  File "ads/bsyeti/big_rt/cli/lib/__init__.py", line 430, in check_and_try_fix_cs_path
    assert len(candidates) == 1, "Not exactly one matching candidate. Candidates {}".format(
AssertionError: Not exactly one matching candidate. Candidates ['MasterBalancer', 'lb_iva_bar_navig_bar_navig_log', 'lb_iva_bigb_market_offers', ......., 'ytsorted_service_log_orders']
```

```
$ ./bb_cluster_analyzer caesar_resharder discover_shard 10 --input .*bs_chevent.*
bootstrap-caesarresharder1-18.vla.yp-c.yandex.net
```
