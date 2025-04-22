This program is designed to aggregate MapKit access logs, and publish statistics to APIKeys service.

## Description

Program has three modes:
  * `preprocess` to filter access logs and aggregate the usage statistics per APIKEY per device id and store it as separate table
  * `push` to upload aggregated statistics to APIKEYS.
  * `push_delayed` - create_delayed_counter statistics with specified date.
There are common parameters:  `--input-dir`, ` --otput-dir`, `--yt-pool`, `--table`, `--yt-cluster`.
Also there are custom parameters for mode. For mode push it's `--apikeys-host` and `--counters`.
With the `--counters` parameter, the push or push_delayed modes can be used to push to APIKEYS from an arbitarry YT table having columns `apikey` and `{counter_name}`,


Usage is the following:
```
    preprocess_mapkit_logs [common pararmeters] MODE [custom parameters]
```
Examples:
```
./preprocess_mapkit_logs --input-dir //logs/maps-core-mobile-access-log/1d --output-dir //home/b2bgeo/data/apikeys/processed_mapkit_logs/test --table 2020-09-02 --yt-cluster hahn preprocess

export APIKEYS_SERVICE_TOKEN="abcdef"
./preprocess_mapkit_logs --input-dir //home/maps/users/4c4d/b2bgeo/data/apikeys/processed_mapkit_logs --table 2020-09-02 --yt-cluster hahn --yt-pool b2bgeo push --apikeys-host apikeys-ipv6.yandex.net
```

By default program tries to process table with name equal to yesterdays' date. To process table for another day, use `--table` parameter.

## Manual runs

Program can be compiled using `ya make` and executed locally.
**NOTE**: you should compile and execute it on Linux host, otherwise it will not be able to start YT task.

## Deployment and production mode

In "production mode" program is executed in sandbox:
  * [preprocess mapkit_logs](https://sandbox.yandex-team.ru/scheduler/24543)
  * [push mapkit_logs](https://sandbox.yandex-team.ru/scheduler/24291)
  * [push monitoring_locations and monitoring_vehicles](https://sandbox.yandex-team.ru/scheduler/43399)
  * [push vrp_locations and vrp_vehicles](https://sandbox.yandex-team.ru/scheduler/44644)

YA_EXEC task is used to compile and execute program using specified revision (see "Svn url for arcadia" parameter).
Do not forget to update revision after your commit.

In case of failures, `preprocess` part can be executed second time.
In case of failures, `push_delayed` part can be executed second time.
Execution of `push` part is dangerous, and in case of failures, we should investigate the reasons, and try to avoid problems during pushing statistics.
One could debug `push` part locally by creating a separate table containing counters only for our own keys.

## Logs location

Currently mapkit logs are taken from [hahn.//logs/maps-core-mobile-access-log/1d]((https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-core-mobile-access-log/1d))
Counters are stored in [hahn.//home/b2bgeo/data/apikeys/preprocessed_mapkit_logs]((https://yt.yandex-team.ru/hahn/navigation?path=//home/b2bgeo/data/apikeys/processed_mapkit_logs))
