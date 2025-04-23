# python_app

Шаблон приложения на python для разворачивания в RTC (RunTime Cloud).
Используются Flask + gunicorn.

## Development

### Tests
Запустить тесты:
```
ya make -rt
```

### Run
```
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


warehouse-report.tst.vs.market.yandex.net:17051/yandsearch?place=print_doc&req_attrs=qdata&feed_shoffer_id=201677878-test-mboc-from-stroller-fbs3