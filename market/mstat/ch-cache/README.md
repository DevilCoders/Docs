# python_app

https://wiki.yandex-team.ru/market/projects/marketstat/support/ch-cache/

Приложение на python для кеширования запросов ODBC->CHaaS разворачивания в RTC (RunTime Cloud).
Используются Flask + gunicorn.


## Development

### Tests
Запустить тесты:
```
ya make -rt
```

### Run
```
export CH_CACHE_SECRET='{"redis_password":"..."}'
./run --port 2606
```

### Deploy
1. ```ya package pkg.json```
2. ```ya upload --type={TASK_TYPE} {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"


## API

### /ping
<pre>
```
@laptop:~$ curl -sD- localhost:2606/ping
HTTP/1.1 200 OK
Server: gunicorn/19.6.0
Date: Mon, 28 May 2018 09:43:58 GMT
Connection: keep-alive
Content-Type: text/plain; charset=utf-8
Content-Length: 4
X-HOST:
X-TIME: 0

0;ok
```
</pre>

### /status

<pre>
```
@laptop:~$ curl -sD- localhost:2606/status
HTTP/1.1 200 OK
Server: gunicorn/19.6.0
Date: Mon, 28 May 2018 09:44:21 GMT
Connection: keep-alive
Content-Type: application/json; charset=utf-8
Content-Length: 238
X-HOST:
X-TIME: 0

{
  "args": {
    "dc": null,
    "debug": true,
    "environment": null,
    "host": "[::1]",
    "logfile": null,
    "port": 2606,
    "statefile": "./state.json",
    "workers": 1
  },
  "opened": true,
  "version": 3647500
}
```
</pre>

### /open

### /close

### usage
```
SCHEMA='http'
CH_HOSTNAME='localhost:1234'
SCHEMA='https'
CH_HOSTNAME='mstat-ch-cache.tst.vs.market.yandex.net'
CH_HOSTNAME='mstat-ch-cache.vs.market.yandex.net'
CH_PASSWORD=''
REDIS_PASSWORD=''

curl --insecure -XPOST -g  "${SCHEMA}://${CH_HOSTNAME}/cache_reset?table=cubes_clickhouse__cube_cpc_clicks_b2b_analyst"
curl --insecure -XPOST -g -d 'show tables;'  "${SCHEMA}://cubes:${CH_PASSWORD}@${CH_HOSTNAME}/?database=cubes"
curl --insecure -XPOST -g -d@test_query.sql  "${SCHEMA}://cubes:${CH_PASSWORD}@${CH_HOSTNAME}/?database=cubes"
curl --insecure "${SCHEMA}://${CH_HOSTNAME}/cache_info"
curl --insecure -XPOST -g -d 'select * from cubes_clickhouse__cube_cpc_clicks_b2b_analyst limit 3'  "${SCHEMA}://cubes:${CH_PASSWORD}@${CH_HOSTNAME}/?database=cubes&count_distinct_implementation=uniqCombined&default_format=ODBCDriver2"

curl --insecure -XPOST -g -d 'show tables;' 'https://cubes:${CH_PASSWORD}@man-uo3jdvyywi8hq8b4.db.yandex.net:8443/?database=cubes'


host=$(redis-cli -h man-8wsasqddshhv3sdf.db.yandex.net -p 26379 sentinel get-master-addr-by-name mstat_ch_cache | head -n 1)
redis-cli -h $host -a ${REDIS_PASSWORD} KEYS '*'
```

### Release
Будучи под SOX компонент требует 2х аппрувов на изменения, что контролируется соответствующим кубом в релизном пайплайне в ЦУМ.
