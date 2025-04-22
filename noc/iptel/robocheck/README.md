# Ext Number Robocheck

Шедулер мониторнга внешних номеров

## Переменные окружения

1. `YENV_TYPE` - выбираем конфиг подключения к БД. Один из: `local`, `docker`, `pgaas`.
1. `DB_HOST` - Переопределяем хост БД в конфиге.
1. `DB_NAME` - Переопределяем имя БД в конфиге.
1. `DB_USER` - Переопределяем пользователя БД в конфиге.
1. `DB_PASSWORD` - Переопределяем пароль БД в конфиге.
1. `TENANT_CODES` - Коды обслуживаемого тенантов через запятую.
1. `EXT_NUMBER_MON_HOST` - Хост сервиса ext-number-mon https://wiki.yandex-team.ru/noc/office/extnummonitor/
1. `EXT_NUMBER_MON_SSL_CAFILE` - Путь до бандла сертефикатов Яндекса
1. `SOLOMON_HOST` - Хост сервиса Solomon https://wiki.yandex-team.ru/solomon/
1. `SOLOMON_TOKEN` - OAuth токен сервиса Solomon
1. `SOLOMON_SSL_CAFILE` - Путь до бандла сертефикатов Яндекса (только для локальной отладки)
1. `EBN_HOST` - Хост API Единой Базы Номеров https://ebn.tel.in.yandex-team.ru/api
1. `GEO_HOST` - Хост Гео Базы https://geoexport.yandex.ru/
1. `JUGGLER_HOST` - Хост API Juggler http://juggler-api.search.yandex.net
1. `JUGGLER_TOKEN` - OAuth токен Juggler `AQAD-***`

## Локальная разработка
Для локальной разработки подготовлен `docker-compose.yml` и `Makefile`
```
make backend
```
В директории `sql` расположены два скрипта: `init.sql` для инициализации БД и
`data.sql` с тестовыми данными для локальной разработки

Для подключения к локальному докеру ЕБН используем:
```
make backend-ebn-docker
```

Для подключения к тестовому стенду ЕБН в деплое используем:
```
sudo ip6tables -t nat -A POSTROUTING -s  fde1:0e04:6409:04d7::/64 ! -o docker0 -j MASQUERADE
make backend-ebn-test
```
