# Результаты бенчмарка

```
ulimit -n 100000
ya make -r && ./transport
```

```
Посылаем тысячу запросов из NetworkThreads и в сервере обрабатываем эти запросы в пуле размером ServerThreads (обрабатываем синхронно в случае, если 0 тредов).

------------------------------------------------------------------------------------
Benchmark                                          Time             CPU   Iterations
------------------------------------------------------------------------------------
BMOneNetworkNoServerThreads/real_time            139 ms         24.1 ms          106
BMOneNetworkOneServerThreads/real_time           145 ms         47.0 ms           96
BMOneNetworkFourServerThreads/real_time          159 ms         70.0 ms          105
BMFourNetworkNoServerThreads/real_time          80.4 ms          143 ms          162
BMFourNetworkOneServerThreads/real_time         80.4 ms          222 ms          176
BMFourNetworkTwoServerThreads/real_time         97.8 ms          270 ms          109
BMFourNetworkThreeServerThreads/real_time        113 ms          315 ms          115
BMFourNetworkFourServerThreads/real_time         451 ms          361 ms          101
BMFourNetworkEightServerThreads/real_time        436 ms          442 ms          145
BMNehFourThreads/real_time                      57.3 ms          516 ms          257
```
