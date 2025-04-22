# PostgreSQL

## DSN

В конечном счёте DSN для production и testing деплойментов должен выглядеть следующим образом:

```
host=host-1,host-2,host-3 \
port=6432 \
dbname=mydb \
user=username \
password=secret \
sslmode=verify-full \
sslrootcert=/path/to/root/cert.crt \
statement_cache_mode=describe \
target_session_attrs=read-write
```

Пояснение к некоторым опциям:

- `host` - при деплое с PostgreSQL в MDB нужно указать все узлы master/slave-кластера
- `statement_cache_mode=describe` - в MDB используется PgBouncer в режиме **transaction pooling**, с которым возникают
  проблемы с поддержкой стандартных go-типов в качестве SQL-аргументов:
  [Fallback valuer option](https://github.com/jackc/pgx/issues/723). Решением проблемы является включение statement
  cache
- `target_session_attrs=read-write` - нужно в master/slave-кластере зафорсить использование соединения c master-узлом,
  чтобы демон мог писать в базу, иначе будут ошибки вида:
  ```
  ERROR: cannot execute INSERT in a read-only transaction (SQLSTATE 25006)"
  ```

## Таймзона

При создании пула указывается рантаймовая переменная для указания таймзоны в соединениях:

```go
cfg.ConnConfig.RuntimeParams["timezone"] = "Europe/Moscow"
```

Это нужно в первую очередь для отсутствия diff-ов в snapshot-тестах: независимо от настроек базы тип данных
`timestamp with time zone` будет сохраняться в одной таймзоне.
