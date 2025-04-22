**Не предназначено для использования в бою!**

## Полезные запросы

#### Проверить, что не разъехались структуры

```sql
SELECT * FROM mail.check_counters(:uid)
 name | broken
------+--------
(0 rows)
```

#### Ищем что происходило с `mid` по `change_log`

```sql
SELECT type, change_date
  FROM mail.change_log
 WHERE uid = :uid
   AND EXISTS (
    SELECT 1
      FROM jsonb_array_elements(changed) c
     WHERE (c->>'mid')::bigint = :mid);
  type  |          change_date
--------+-------------------------------
 store  | 2017-04-10 05:08:36.716782+03
 update | 2017-04-10 13:14:52.340496+03
 move   | 2017-04-10 13:19:39.577593+03
 delete | 2017-04-10 13:19:46.489136+03
(4 rows)
```

вариант с использованием [оператора `@>` json](https://www.postgresql.org/docs/9.6/static/functions-json.html#FUNCTIONS-JSONB-OP-TABLE)
съест меньше CPU

```sql
SELECT type, change_date
  FROM mail.change_log
 WHERE uid = :uid
   AND changed @> '[{"mid":163536961468891138}]';

  type  |          change_date
--------+-------------------------------
 store  | 2017-10-09 14:06:38.198842+03
 update | 2017-10-09 14:06:38.252132+03
(2 rows)
```

## Работа с метаданными

#### Отфильтровать `recipients` по типу (`mail.recipient_type`)
[MAILPG-1023](https://st.yandex-team.ru/MAILPG-1023)

`->` фильтруем массив реципиентов по типу

```sql
SELECT recipients->'to', subject FROM mail.messages WHERE uid = :uid;
                                 ?column?                                  |              subject
---------------------------------------------------------------------------+-----------------------------------
 {"(to,Reader,Reader@Shakespeare)"}                                        | Кто здесь?
 {"(to,Reader,Reader@Shakespeare)","(to,Бернардо,бернардо@Shakespeare)"}   | Нет, сам ты кто, сначала отвечай.
 {"(to,Reader,Reader@Shakespeare)","(to,Франциско,франциско@Shakespeare)"} | Да здравствует король!
```

`->>` достаёт один элемент из массива реципиентов с заданным типом

```sql
SELECT recipients->>'from', subject FROM mail.messages WHERE uid = :uid;
                ?column?                |              subject
----------------------------------------+-----------------------------------
 (from,Бернардо,бернардо@Shakespeare)   | Кто здесь?
 (from,Франциско,франциско@Shakespeare) | Нет, сам ты кто, сначала отвечай.
 (from,Бернардо,бернардо@Shakespeare)   | Да здравствует король!
```

#### Достать пары `(label.name,label.type)` по `box.lids`

В ручных запросах [неудобно](https://paste.yandex-team.ru/234524)
делать дополнительный подзапрос в `labels`,
а знать какие метки стоят на письмах нужно.

Функция (как и колонка `box.labels`) **не предназначена** для использования в бою,
тк ходит в `labels`, для каждого вызова.

```sql
SELECT mid, lids, code.labels_by_lids(uid, lids) from mail.box where uid = :uid;
        mid         |  lids  |        labels_by_lids
--------------------+--------+-------------------------------
 162129586585337857 | {9}    | {"(yaru,domain)"}
 162129586585337858 | {11}   | {"(17,type)"}
 162129586585337859 | {9,11} | {"(yaru,domain)","(17,type)"}
(3 rows)
```

Используя [виртуальную колонку][momjian-virual-column] `box.labels` (задание `alias` обязательно)

```sql
SELECT mid, lids, box.labels FROM mail.box WHERE uid = :uid;
        mid         |  lids  |            labels
--------------------+--------+-------------------------------
 162129586585337857 | {9}    | {"(yaru,domain)"}
 162129586585337858 | {11}   | {"(17,type)"}
 162129586585337859 | {9,11} | {"(yaru,domain)","(17,type)"}
(3 rows)
```

[momjian-virual-column]: http://momjian.us/main/blogs/pgblog/2013.html#April_1_2013 "Creating Virtual Columns"
