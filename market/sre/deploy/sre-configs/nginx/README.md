# Переменные окружения шаблонов для конфигов nginx #

Все переменные окружения вкладываются через объект `env`.

Пример использования в шаблонах:

`listen {{ env.NGINX_PORT }};`

Вывод будет примерно таким:

```
env.NGINX_ACCESS_LOG_OFF             # выключить access.log
env.NGINX_CLIENT_MAX_BODY_SIZE       # директива client_max_body_size
env.NGINX_INCLUDES                   # список инклудов в default.conf шаблоне, задается списком
env.NGINX_LOG_BUFFER_ENABLED
env.NGINX_LOG_BUFFER_FLUSH
env.NGINX_LOG_BUFFER_FLUSH_ENABLED
env.NGINX_LOG_BUFFER_SIZE
env.NGINX_LOG_PREFIX
env.NGINX_PORT                       # порт по умолчанию
env.NGINX_PORT_HTTP                  # используется в случае, когда хочется http и https
env.NGINX_PROXY_BUFFERING
env.NGINX_PROXY_CONNECT_TIMEOUT
env.NGINX_PROXY_READ_TIMEOUT
env.NGINX_PROXY_SEND_TIMEOUT
env.NGINX_UPSTREAM_PORT
```




