# Трансфер как сервис

Что требуется:
====
* Директория /var/log/husky с правами на добавление файлов для пользователя husky:husky
* Доступ к боевому окружению - хостам, указанным в модуле ora2pg.configs.prod.yaml
* Если хочется запустить в другом окружении - создаем файлик /etc/default/husky.yaml, пишем туда имя окружения
* БД huskydb
* Если хочется sentry (а оно вам хочется), то:
   * нужно добавить `dsn` `(Settings->Client Keys)` в `sentry_dsn: '...'` в конфиг файл или переменную окружения `SENTRY_DSN`.
   * можно добавить `sentry_log_level: 30` ([чиселко](https://docs.python.org/2/library/logging.html#logging-levels)) в конфиг или `SENTRY_LOG_LEVEL`. По умолчанию `40` -- `logging.ERROR`

Как работать:
====

* Запускаем сервис
```
$ service husky start
```
* Заливаем пользователей, ожидающих переноса. Указываем список пользователей, целевую базу, флаги. Можно задать приоритет пользователей через поле priority - меньшее значение соответствует высокому приоритету.
```
huskydb=# \df code.add_users_in_dogsleds
List of functions
-[ RECORD 1 ]-------+-----------------------------------------------------------------------------------------------
Schema              | code
Name                | add_users_in_dogsleds
Result data type    | integer
Argument data types | i_uids bigint[], i_to_db text, i_disallow_inited boolean DEFAULT false, i_fill_change_log boolean DEFAULT false, i_update_mail_migration boolean DEFAULT false, i_husky_id integer DEFAULT NULL::integer, i_priority integer DEFAULT 0
Type                | normal

huskydb=# select * from code.add_users_in_dogsleds(ARRAY[1,2,3,4,5], 'postgre:1', false, true, false, 2);
 add_users_in_dogsleds
-----------------------
                     5
huskydb=# select * from code.add_users_in_dogsleds(ARRAY[3000340793], 'oracle:ymail/ympass@mdb302', false, true, false, 2);
 add_users_in_dogsleds
-----------------------
                     1

(1 row)
```
* Пользователи появляются в табличке transfer.users_in_dogsleds со статусом 'pending'.
```
huskydb=# select * from transfer.users_in_dogsleds ;
-[ RECORD 1 ]---------+------------------------------
uid                   | 1
to_db                 | postgre:1
disallow_inited       | f
fill_change_log       | t
update_mail_migration | f
priority              | 0
tries                 | 0
status                | pending
last_update           | 2015-09-11 13:18:27.173969+03
try_notices           |
...
-[ RECORD 6 ]---------+------------------------------
uid                   | 3000340793
to_db                 | oracle:ymail/ympass@mdb302
disallow_inited       | f
fill_change_log       | t
update_mail_migration | f
priority              | 0
tries                 | 0
status                | pending
last_update           | 2015-09-11 13:45:46.902562+03
try_notices           |
```
* Когда husky дойдет до этих записей, он вычитает их, проставив статус 'in_transfer' и раздаст их своим подпроцессам для переноса. В результате успешной попытки переноса выставляется статус 'complete', в результате неуспешной - возвращается статус 'pending' и в try_notices пишется краткое сообщение об ошибке (на текущий момент - строчка кода и исключение). При превышении максимального числа попыток выставляется статус 'error'
```
huskydb=# select * from transfer.users_in_dogsleds;
-[ RECORD 1 ]---------+---------------------------------------------------------------------------------------------------
uid                   | 3000340793
to_db                 | oracle:ymail/ympass@mdb302.yandex.ru
disallow_inited       | f
fill_change_log       | t
update_mail_migration | f
priority              | 0
tries                 | 1
status                | complete
last_update           | 2015-09-11 13:52:00.373953+03
try_notices           | {NULL}
-[ RECORD 2 ]---------+---------------------------------------------------------------------------------------------------
uid                   | 1
to_db                 | postgre:1
disallow_inited       | f
fill_change_log       | t
update_mail_migration | f
priority              | 0
tries                 | 3
status                | error
last_update           | 2015-09-11 13:47:27.452788+03
try_notices           | {"/home/prez/wmi_build/src/mdb/ora2pg/blackbox.py:91, in _black_request:raise exc","/home/prez/wmi_build/src/mdb/ora2pg/blackbox.py:91, in _black_request:raise exc","/home/prez/wmi_build/src/mdb/ora2pg/blackbox.py:91, in _black_request:raise exc"}
...
```
* And... it's gone!
