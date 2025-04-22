# Configuring through config file

Example config (cfg.pb.txt):
```
MyConfig {
    HeavyPath: "../heavy.serialized"
    LightPath: "../light.serialized"
    StatsPath: "../place_stats.serialized"
}
```

Launching server:
```
$ ./shiny_server -c cfg.pb.txt -p 2228

INFO: 2022-02-16 11:12:41.062 +0300 query_handler.cpp:10 Entries in heavy table: 1000
INFO: 2022-02-16 11:12:41.062 +0300 query_handler.cpp:11 Entries in light table: 1000
INFO: 2022-02-16 11:12:41.062 +0300 query_handler.cpp:12 Entries in stats table: 94
2022-02-16T11:12:41+0300        INFO    Shiny daemon has started with pid: 26867
2022-02-16T11:12:41+0300        INFO    Http handlers init
2022-02-16T11:12:41+0300        INFO    Http server starting
2022-02-16T11:12:41+0300        INFO    Http server started at 2228 port
```

# Configuring through command line

```
$ ./shiny_server --my-stats-path ../place_stats.serialized --my-heavy-path ../heavy.serialized --my-light-path ../light.serialized -p 2228
INFO: 2022-02-16 12:11:21.866 +0300 query_handler.cpp:10 Entries in heavy table: 1000
INFO: 2022-02-16 12:11:21.867 +0300 query_handler.cpp:11 Entries in light table: 1000
INFO: 2022-02-16 12:11:21.867 +0300 query_handler.cpp:12 Entries in stats table: 94
...
```

# Querying
```
$ curl localhost:2228/nth?n=0\&table=heavy
{"FullElapsed":170104,"HeavyPlace":"offerinfo"}
$ curl localhost:2228/nth?n=0\&table=light
{"FullElapsed":0,"LightPlace":"consistency_check"}
$ curl localhost:2228/nth?n=1000\&table=heavy
"n is too big" $ curl localhost:2228/nth?n=999\&table=heavy
{"FullElapsed":74092,"HeavyPlace":"model_bids_recommender"}
$ curl localhost:2228/nth?n=999\&table=light
{"FullElapsed":0,"LightPlace":"consistency_check"}
$ curl localhost:2228/nth?n=999\&table=stats
"can't compute query for such table"
$ curl localhost:2228/placestat?place=model_bids_recommender
{"MaxElapsed":101209,"MinElapsed":3,"P50":504.9286724,"P70":868.5633946,"P90":3749.828509,"P95":10308.63029,"P99":34119.2201,"P9999":92660.24649,"Place":"model_bids_recommender"}
$ curl localhost:2228/placestat?place=consistency_check
{"MaxElapsed":126606,"MinElapsed":0,"P50":0,"P70":1,"P90":4,"P95":5,"P99":6.706531183,"P9999":107.7600526,"Place":"consistency_check"}
```
