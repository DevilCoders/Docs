# Solomon Pusher

Планируем перевезти сюда джобы соломон пушера<br />

Написан на основе [apscheduler](https://apscheduler.readthedocs.io/en/latest/index.html), [ylock](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/ylock/README.md), [ylog](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/ylog/README.md)

Все питоновские задачки пишем [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/solomon-pusher/lib/jobs.py).

После этого добавляем их в [json-файл](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/solomon-pusher/lib/configs/jobs.json) в виде записи 
```
 {
     "func": "lib.jobs:lslah", 
     "trigger": "interval", 
     "seconds": 15, 
     "name": "Test lslah with is lslah", 
     "id": "lslah"
}
``` 
Где:
- `func` - референс-ссылка на функцию
- `trigger` - тип триггера [`date`](https://apscheduler.readthedocs.io/en/latest/modules/triggers/date.html#module-apscheduler.triggers.date), [`interval`](https://apscheduler.readthedocs.io/en/latest/modules/triggers/date.html#module-apscheduler.triggers.date), [`cron`](https://apscheduler.readthedocs.io/en/latest/modules/triggers/cron.html#module-apscheduler.triggers.cron)
- `name` - описание джобы
- `id` - уникальный идентификатор джобы в рамках инстанса

Все задачки запускаются с локом в зукипере. Лок вешается на весь кластер на задачу. Если задачка повиснет, то через 600 секунд лок будет сброшен

Логи пишутся исходя из [конфига](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/solomon-pusher/lib/configs/production/logging.json)

## Development

### Tests
Запустить тесты:
```
ya make -rt
```

local `lib/configs/local/app.json`
```json
{
  "ylock": {
    "backend": "zookeeper",
    "config": {
      "hosts": [
        "mzoo01et.market.yandex.net",
        "mzoo01ft.yandex.ru",
        "mzoo01ht.yandex.ru"
      ],
      "connect_timeout": 10,
      "prefix": "solomon-pusher/jobs"
    }
  }
}
```

### Run
```
./run --port 26062 --env=local --datasource=$HOME"/Projects/arcadia/market/logistics/solomon-pusher/lib/configs/local/app.json"
```

Параметр `--datasource` обязателен

### Deploy (deprecated)
1. ```ya package pkg.json```
2. ```ya upload --type={TASK_TYPE} {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"

UPD: сейчас собирается через пайплайн

### TSUM release machine

- [/delivery/delivery-dashboard/solomon-pusher](https://tsum.yandex-team.ru/pipe/projects/delivery/delivery-dashboard/solomon-pusher)

### Nanny services

- [production_market_solomon_pusher_iva/](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_iva/) 
- [production_market_solomon_pusher_sas/](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_vla/) 
- [production_market_solomon_pusher_vla/](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_sas/) 


The services have been collected on a dashboard [market_solomon_pusher](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_solomon_pusher/)

### YASM dashboards will be available soon
- [market-nginx/itype=marketdeliverysolomonpusher](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketdeliverysolomonpusher;ctype=production;prj=market/) 
- [market-porto/itype=marketdeliverysolomonpusher](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdeliverysolomonpusher;ctype=production;prj=market/)

## API

### /monitoring

Показывает, что шедуллер запущен и работает. Может отвечать
- `0;ok` - работает и запущен
- `1;stopped` - остановлен шедуллер
- `2;paused` - приостановлен

<pre>
```
@laptop:~$ curl -sD- localhost:2606/monitoring
HTTP/1.1 200 OK
Server: gunicorn/19.6.0
Date: Mon, 28 May 2018 09:43:58 GMT
Connection: keep-alive
Content-Type: text/plain; charset=utf-8
Content-Length: 4
X-HOST: 
X-TIME: 0
```
</pre>


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
