**Что это?**

Простой текстовый key-value сторадж для хранения произвольных данных

Кэш содержит записи ` (uid: uint64, key: str, datatype: str, value: str)`

Первичный ключ ` (uid, key, datatype)`

`datatype` - вспомогательное поле, в котором можно хранить метадату для `value`


**Интерфейс:**

`reqId` - идентификатор запроса

`Optional<Value> get(uid, key, datatype, reqId)` - получает значение из кэша для `uid`. Возвращает `Null` если значение не найдено

`bool put(uid, key, datatype, value, reqId)` - сохраняет значение `value`. Возвращает `true` в случае успеха и `false` если значение уже есть в кэше

**QueryConf:**

https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_cachedb/cachedb.conf

**Логи:**

Логи пишутся в tskv формате с помощью `logdog` в формате `mail-cachedb-tskv-log`

**Общие настройки:**

```
logger: name_of_logger     # имя логера в платформе
default_datatype: datatype # тип по умолчанию для get и put методов
reactor: global            # реактор для запуска
```

**Реализация Postgres**

Кэш над базой в yandex cloud

Production: https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdbro0nkrsr3nnk5srsl

Prestable: https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdb7vntphipnbi8mi6ls

Для походов в базу используется `pgg`. Выбор мастера или реплики происходит через `target_session_attrs` (в конфиге указывать не надо). Для `get` в строку подключения добавляется `target_session_attrs=any`. Для `put` в строку подключения добавляется `target_session_attrs=read-write`. Пароль для базы данных либо пробрасывается через стандартные стредства `libpq` (файл `.pgpass` или connection string), либо через параметр конфига `.pg.password_file`, который содержит пароль (добавится в конец connection string). При логировании connection string пароль замазывается. Модуль умеет профилировать запросы через `mail/pa`, но сам профайлер в модуле не создаётся. Настройки `.pg` проксируются в фабрику создания коннектов в `pgg`

Пример модуля:
```
system:
    name: cachedb
    factory: ymod_cachedb::Postgres
configuration:
    logger: name_of_logger
    defaut_datatype: datatype
    reactor: global
    pg:
        log_pa: true
        max_connections: 20 
        max_total_pools_capacity: 0
        queue_timeout_ms: 100
        connect_timeout_ms: 500
        query_timeout_ms: 1000
        query_conf: etc/cachedb/cachedb.conf
        connection_string: 'host=man.db.yandex.net,sas.db.yandex.net,vla.db.yandex.net port=6432 dbname=cachedb user=cachedb'
        password_file: path/to/plain_text_password
        user: sendbernar
        async_resolve: true
        ipv6_only: true
        dns_cache_ttl_sec: 120
```

**Реализация Dummy**

Модуль-заглушка, которая ничего не находит и никуда не пишет. На любой `get` возвращается пустота, на `put` возвращается значение из конфига `.dummy.put_status`. Модуль предназначен для случаев, когда надо резко прекратить походы в кэш из-за какого-либо факапа

Пример модуля:
```
system:
    name: cachedb
    factory: ymod_cachedb::Dummy
configuration:
    logger: name_of_logger
    defaut_datatype: datatype
    reactor: global
    dummy:
        put_status: true
```
