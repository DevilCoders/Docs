# DNS

## Описание

Плагин отвечает за обновление/удаление записей в `DNS` для всех объектов racktables. А так же за выгрузку зон в
экспортную ручку `export/zones.xml`.

## Как работает

### Полный ресинк каждый час (`resync_db` + `dnsapi_sync` + `apply_dnsapi_changes`)

Запускается по крону, собирает все желаемые записи в `DNS`, и обновляет в базе таблицу `Yandex_DNS`. В этой табличке
находится полный стейт всего что `RT` хочет в `DNS` и то, что в `DNS` на самом деле есть.

Описание стейта каждой записи [см ниже](#Yandex_DNS_table).

После этого запускается импорт дампа из `dns2api` по `http`. В этом дампе абсолютно все записи Яндекса в `DNS`, оттуда
выкидывается всё неинтересное и не связанное с `noc` и `RT`. По анализу этого дампа можно понять что на самом деле находится
в `DNS` (у записей в бд проставляется стейт `live`, например). Всё что есть в дампе в интересных для `RT` зонах
(например `.yndx.net`), но при этом отсутствующее в `RT` считается мусором (т.е. `garbage`). Мусор удаляется
автоматически для зоны `.dhcp.yndx.net`, для всех остальных - только вручную (по крайней мере пока так,
вероятно это изменится в будущем).

Финальным шагом является `apply_dnsapi_changes`, которая с разными ретраями пробует применить изменения в `DNS`
через `dns2api` для всех не-`live` записей.

Логи находятся здесь: `/var/log/rtdns/sync.log` (на мастер-ноде `RT`).

### Обновление в **DNS** при изменении объектов

Плагин вешается хуками на:

 - изменение `fqdn`
 - изменение `ip`
 - удаление объекта

В этот момент для 1 объекта происходит полный ресинк его записей в `DNS`. Т.е. обновляется как стейт в `Yandex_DNS`
таблице так и сразу будет попытка отправить все изменения через `dns2api`. Т.е. у каждой записи есть `origin`, то
гарантированно можно выкинуть все старые записи объекта из `DNS`, даже если в момент вызова хука их уже нет.

### Таблица **Yandex_DNS** {#Yandex_DNS_table}

Поля с комментариями (в `plugins/dns/plugin.php`):

```
-- type-name-data is a private key
-- e.g. A-mcsl.yndx.net-1.2.3.4
`type` ENUM("A", "AAAA", "PTR", "CNAME") NOT NULL,
`name` VARCHAR(255) NOT NULL,
`data` VARCHAR(255) NOT NULL,

-- hint where this record come from
`origin` VARCHAR(255) NULL,

-- dns zone
`zone` VARCHAR(255) NOT NULL,

-- extra flags
`flags` ENUM("dynamic", "other", "ptr-no-ptr-nets") NULL,

-- record state:
--  - draft: just created
--  - applied: change applied to dns
--  - live: found dns record to be LIVE on dns servers (this check made every 1hr)
--  - drop: do not needed anymore, should be removed from DNS soon
-- all state transitions are possible, but reaction is:
--  - draft: we will send query to DNS and set applied if we get 200 OK
--  - applied: we will check record existence on DNS servers periodiccally and set live once found
--  - live: we periodically recheck records existance on DNS and move back to draft if missing
--  - drop: we will issue delete requests to DNS until we dont found record on DNS servers anymore.
--          Finally record will be removed (i.e. drop->null)
`state` ENUM("draft", "applied", "live", "drop") NOT NULL DEFAULT "draft",

-- status hint what is going on. Here will be errors during updates if any
`status` VARCHAR(255) NOT NULL DEFAULT "",

-- timestamp record was first created
`ts_created` DATETIME(0) NOT NULL DEFAULT CURRENT_TIMESTAMP,

-- timestamp record was last checked on DNS servers
`ts_checked` DATETIME(0) NULL DEFAULT NULL,

-- timestamp we last tryed to apply in dnsapi
`ts_apply` DATETIME(0) NULL DEFAULT NULL,

-- how much we tried (failed) and how much we
`cnt_apply_tries` INT NOT NULL DEFAULT 0,
```

### Статистика и дебаг

Пока нет джагглерных ивентов совсем, мониторится всё руками через бд примерно так:

```
mysql> select * from (select count(*) as count, if(state = "live", state, concat(if(origin = 'garbage', concat("(garbage) ", state), state), " [", type, "]")) as state from Yandex_DNS group by 2) as x order by x.state asc; -- stats
+--------+------------------------+
| count  | state                  |
+--------+------------------------+
|     24 | (garbage) drop [A]     |
|     15 | (garbage) drop [AAAA]  |
|      1 | (garbage) drop [CNAME] |
|  27773 | (garbage) drop [PTR]   |
|    265 | draft [PTR]            |
|      5 | drop [PTR]             |
| 530104 | live                   |
+--------+------------------------+
7 rows in set (1.02 sec)
```

Можно так же легко вытащить всё что должно быть в `DNS` с точки зрения `RT` для каждого объекта, например:

```
mysql> select * from Yandex_DNS where origin = 'object:80000';
+-------+-----------------------+-------------------------------------+--------------+------------------------------------------+---------+-------+--------+---------------------+---------------------+---------------------+-----------------+
| type  | name                  | data                                | origin       | zone                                     | flags   | state | status | ts_created          | ts_checked          | ts_apply            | cnt_apply_tries |
+-------+-----------------------+-------------------------------------+--------------+------------------------------------------+---------+-------+--------+---------------------+---------------------+---------------------+-----------------+
| AAAA  | mcsltest-me1.yndx.net | 2a02:6b8:b010:88:216:3eff:fe62:c535 | object:80000 | yndx.net                                 | dynamic | live  |        | 2022-04-27 12:53:47 | 2022-06-02 22:32:21 | 2022-06-01 21:07:55 |               0 |
| AAAA  | mcsltest.yndx.net     | 2a02:6b8:b010:88:216:3eff:fe62:c536 | object:80000 | yndx.net                                 | dynamic | live  |        | 2022-04-27 12:53:47 | 2022-06-02 22:32:21 | 2022-06-01 21:07:56 |               0 |
| PTR   | mcsltest-me1.yndx.net | 2a02:6b8:b010:88:216:3eff:fe62:c535 | object:80000 | 8.8.0.0.0.1.0.b.8.b.6.0.2.0.a.2.ip6.arpa | NULL    | live  |        | 2022-04-27 12:53:47 | 2022-06-02 22:32:21 | 2022-06-01 21:07:55 |               0 |
| PTR   | mcsltest.yndx.net     | 2a02:6b8:b010:88:216:3eff:fe62:c536 | object:80000 | 8.8.0.0.0.1.0.b.8.b.6.0.2.0.a.2.ip6.arpa | NULL    | live  |        | 2022-04-27 12:53:47 | 2022-06-02 22:32:21 | 2022-06-01 21:07:55 |               0 |
| CNAME | mcsltest.yndx.net     | mcsltest-me0.yndx.net               | object:80000 | yndx.net                                 | dynamic | live  |        | 2022-04-27 12:53:47 | 2022-06-02 22:32:21 | 2022-06-01 21:07:56 |               0 |
+-------+-----------------------+-------------------------------------+--------------+------------------------------------------+---------+-------+--------+---------------------+---------------------+---------------------+-----------------+
5 rows in set (0.00 sec)
```

В базе все `IP` адреса текстом как раз для простоты дебага, кажется тут особо нет смысла экономить место, но
зато очень легко разглядывать =).
