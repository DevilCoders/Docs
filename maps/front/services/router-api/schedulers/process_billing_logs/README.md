
## WITH ANY CHANGES YOU MUST CHECK STATISTICS IN [ADMIN](https://admin-developer.tech.yandex-team.ru)

## process\_billing\_logs
- script to aggregate access logs (MapKit) and publish statistics to ApiKeys service.

It performs the following actions:

  * `prepare` filters access logs, aggregates statistics per APIKEY and stores it in YT table
  * `push` uploads the statistics from the table to Apikeys-int service

The script is successfull if all stages are done. If `prepare` action are failed, it should be restarted.
If `push` action are failed and script began to push statistics to Apikeys we **CAN NOT** restart it, we can not duplicate counters.

**NB:** Don't run more than one `push` instances of the script simultaneously.

Usage:

```bash
    ya make
    ./bin [parameters]
```

Actual help and all parameters:

```bash
    ./bin -h
```

Example - run prepare:

```bash
./bin
    --input-dir //logs/maps-core-mobile-access-log/1d
    --output-dir //home/b2bgeo/data/apikeys/processed_mapkit_logs
    --yt-cluster hahn
    --yt-pool b2bgeo
    --action preprocess
    --action push_stats
    --apikeys-host apikeys-ipv6.yandex.net
```

This `push` script works only on `Linux` because of `Nile`


Example - push statistics to ApiKeys:

```bash
./bin
    --table-path //home/maps/front/router-api/production/2022-05-27T13:05:00
    --apikeys-host http://apikeys-int.tst.c.maps.yandex.net
    --tvm-src 2015949
    --tvm-dst 2006077
```


## Guide when reactions failed

- If it is `prepare` just restart reaction instance
- If it is `push` you have to make sure that no apikey has been pushed. If so, restart reaction instance otherwise skip it
