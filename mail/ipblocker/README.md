# Webmail ipblocker

Тул для майнинга редисок из КХ и добавления их в ЕББ.

Как работает: проверяет лок в YT (чтобы переживать -ДЦ запущен в разных),
раз в sleep секунд запускает query,
отбирает ip адреса с cnt > threshold,
добавляет их в ЕББ в группу `CBB_FLAG` с ttl `CBB_EXPIRE_DELAY`.

## Deploy

https://deploy.yandex-team.ru/stages/mail_ipblocker

## Параметры запуска

```
  --sleep SLEEP         sleep delay in seconds (default: 60)
  --seconds SECONDS     seconds to grep (default: 300)
  --limit LIMIT         query limit (default: 1000)
  --threshold THRESHOLD
                        minimum requests count (default: 5000)
  --dry-run             dry run (don't block, just print ips)
```

## Переменные окружения

### Настройки ЕББ

`CBB_ENDPOINT` — эндпоинт для добавления в ЕББ (https://cbb-ext.yandex-team.ru)

`CBB_EXPIRE_DELAY` — ttl в ЕББ (сек)

`CBB_FLAG` — группа в ЕББ куда добавлять

`TVM_DST`, `TVM_SRC` — tvm dst и src для получения сервис-тикета для авторизации в ЕББ


### Настройки КХ

`CH_HOST`, `CH_PASS`, `CH_USER` — хост, пользователь, пароль

`CH_QUERY` — запрос (например, `select distinct(x_real_ip) as ip, count() as cnt from logs.homer_access_tskv where date = today() and timestamp > now() - {seconds} and timestamp <= now() and x_real_ip != '-' and request ='/homer/' group by ip order by cnt desc limit {limit}`)

### Настройки локов

Используется [механизм блокировок YT](https://yt.yandex-team.ru/docs/description/locking/cypress_as_locking_service)

`YT_TOKEN`, `YT_LOCK` — токен YT и путь до лока (например, `//tmp/webmail_ipblocker`)


### Необходимые сетевые доступы

До КХ.

Для добавления в ЕББ:

`cbb-ext.yandex-team.ru tcp: 443`

Для локов:

`locke.yt.yandex.net tcp: 80, 443`

`_YTNETS_ tcp: 80, 443, 9013`
