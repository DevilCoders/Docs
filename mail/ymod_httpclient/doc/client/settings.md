## Настройки

Пример yaml конфига с комментариями:
```yaml
user_agent: ''  # передается в соответствующем заголовке
enable_logging: false  # включить логирование
tskv_logging: false  # включить TSKV логи
tskv_log_name: ''  # имя TSKV логгера
post_args_logging: false  # логировать тело POST запроса
post_args_log_entry_max_size: 1000  # ограничение на размер записи тела POST в логе
headers_logging: 0  # логировать заголовки запроса
reuse_connection: 0  # включить keep-alive
preffered_pool_size: 100  # размер пула keep-alive соединений
poll_timeout: <duration::max()>  # время жизни keep-alive соединения в пуле
connect_attempt_timeout: 3s  # таймаут на коннект (включая резолв)
default_request_timeout: 15s  # таймаут на весь запрос (включая коннект)
min_request_duration: 0.1ms  # не ретраить, если осталось меньше времени, чем
congestion_control:
    reactor_overload_delay: 5ms # пороговое значение задержки реакторов, после которого начинается троттлинг открытия новых соединений
dns:
    cache_ttl: 0  # при >0 включает кэширование результатов dns запросов, обычно 60s
ssl:
    verify_hostname: 0  # верификация сервера по rfc2818
send_ssl_server_name: 1  # поддержка SNI
```

Без платформы конфигурируется через ```yhttp::client::settings```.
