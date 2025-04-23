## Логирование

В yhttp::client имеется возможность записи каждого запроса в tskv лог. Для этого в платформе нужно создать логгер и включить соответствующие настройки в клиенте.

Пример записи:
```
tskv	tskv_format=httpout-log	timestamp=2020-01-24 19:34:25.820580	timezone=+0300	session_id=0x2d6bf3c80	y_context=PYecR6QjP8c1	host=push.yandex.ru	port=443	uri=push.yandex.ru:443/binary_notify	status=200	resolve_time=0.000	connect_time=0.000	tls_time=0.000	total_time=0.006	error=success	bytes_out=1501	bytes_in=219	attempt=0
```

Настройки логгера:
```yaml
httpout:
    level: info
    format: "tskv\ttskv_format=httpout-log\ttimestamp=%Y-%m-%d %H:%M:%S.%f\ttimezone=+0300\t%v"
    queue_size: 1048576
    sinks: [ { type: file, path: var/log/app/httpout.log } ]
```

Настройки клиента:
```yaml
enable_logging: true  # включить логирование
tskv_logging: true  # включить TSKV логи
tskv_log_name: 'httpout'  # имя TSKV логгера
post_args_logging: true  #  логировать тело POST запроса
post_args_log_entry_max_size: 1000  # ограничение на размер записи тела POST в логе, в байтах
headers_logging: true  # логировать заголовки запроса
protected_log_headers: ["X-Ya-Service-Ticket"] # замазывать значения перечисленных заголовков перед выводом в лог
```

