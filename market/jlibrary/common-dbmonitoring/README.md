# common-dbmonitoring

Библиотека принимает jdbcTemplate, имя схемы и таблицы в качестве параметаров для подключения и отдает события,
понятные для Juggler, которые хранятся в этой таблице. Также, если событие протухло и не было обновлено вовремя, то его
статус в выдаче для juggler меняется на CRIT.

Помогает настроить мониторинги.

Таблица juggler_events создается в схеме монитор в БД. Ее liquibase миграция:

``` postgresql
create schema monitor;

create table monitor.juggler_events
(
    -- 253 is the max length of a hostname (see RFC for more information)
    host                varchar(253)    not null,
    service             text            not null,   --(?)
    status              varchar(4)      not null,   --(?)
    description         text            not null,
    full_description    text            not null,
    update_time         timestamp with time zone not null,
    expire_time         timestamp with time zone not null
);
```
