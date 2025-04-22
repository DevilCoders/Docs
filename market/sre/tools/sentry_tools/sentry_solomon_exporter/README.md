Утилита предназначена для экспорта метрик Sentry в Solomon через http интерфейс.

Для назначения конфига и файла с токеном можно использовать опции командной строки:
```
usage: sentry_solomon_exporter [-h] [--config_file CONFIG_FILE] [--token_file TOKEN_FILE] [--bind_port BIND_PORT] [--bind_address BIND_ADDRESS]

Expose Sentry metrics in Solomon json style

optional arguments:
  -h, --help            show this help message and exit
  --config_file CONFIG_FILE
                        Yaml config file
  --token_file TOKEN_FILE
                        File with secret sentry token. Also you can use SENTRY_TOKEN env var.
  --bind_port BIND_PORT
                        Listen port
  --bind_address BIND_ADDRESS
                        Listen address
```
**Аргументы командной строки имеют приоритет на конфигом.**


В yaml-конфиге, который по дефолту лежит в /etc/sentry/sentry_solomon_exporter.yaml, нужно указать:
> SENTRY_URL_BASE - базовый url, для кластера надо указать localhost

>API_PATH(путь после / ) - в текущей версии это /api/0

>PORT - порт на котором будет слущать сервер

>HOST - хост на котором будет слушать сервер

Так же можно прописать порт и хост на котором будет слушать http сервер.
Пример:
```
SENTRY_URL_BASE: "https://sentry-test.market.yandex-team.ru"
API_PATH: '/api/0/'
PORT: 8001
HOST: 127.0.0.1
```

В конфиге solomon:
```
dvkhromov@sentry01vt:~$ cat /etc/solomon-agent/service.d/sentry.conf
Project: "market"
Service: "sentry"

PullInterval: "60s"

Modules: [
    { HttpPull: {
        Url: "http://localhost:8001/"
        Format: JSON
	TimeoutMillis: 30000
    }}
]
```
