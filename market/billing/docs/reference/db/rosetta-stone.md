# MySQL / Oracle / PostgreSQL

Как соответствуют друг другу разные концепции и команды в MySQL, Oracle, PostgreSQL

## Концепции

### Database, schema { #database-schema }

**Postgres:**
* в одном инстансе PG могут быть несколько `database`, в одной `database` могут быть несколько `schema`
* между `database` джойниться нельзя, между `schema` &mdash; можно
* бекапы настраиваются на уровне `database`

Документация: <https://www.postgresql.org/docs/12/ddl-schemas.html>

**MySQL:**
* в одном инстансе mysql может быть несколько `database`
* между разными `database` можно джойниться


**Oracle:**
* `schema` -- это набор объектов (таблиц, view), принадлежащих одному пользователю (`user`)
* между разными `schema` можно джойниться


Итого mysql-ные `database` &mdash; это как postgres-овые `schema`.
Oracle-овые `schema` тоже похожи на postgres-овые.
* ****

## Правила переноса данных в Postgres

### Обновление батчами
Для корректной работы batchUpdate в `Postgres` необходимо дописать в параметры соединений (пропертю `tms.postgresql.properties`)
 `reWriteBatchedInserts=true`.  В противном случае все инсерты в базу будут выполняться по одному, что займет существенно большее время.
**Примечание:** это правило не работает с `insert... on conflict do update`. В таком случае, преобразователь надо писать вручную. Пример
в <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/stocks/StockDao.java?rev=r8611068#L90>

### Простые типы данных
* **bigint** - применяется для айдишников (всех полей с суффиксом `_id`)
* **numeric(?)** - соответсвует не айдишникам с типам данных number(?), за исключением случая ниже
* **smallint** - применяется там, где точно понятно, что значение поля не выйдет за пределы. Также применяется там,
  где в `Oracle` использовался number(1) в качестве `boolean`
* **varchar** - вместо любого varchar или varchar2 в `Oracle`
### Комплексные типы данных
В `Oracle` существуют комплексные типы данных, созданные для той или иной цели. В `Postgres` были созданы
их аналоги в качестве доменов с именами `ntt_varchar` и `t_number_tbl`. Если в `Oracle` это был тип данных табличного типа, то в
`Postgres` они были преобразованы в массивы. Обращение с массивами данных при помощи этих типов выглядит следующим образом:
```
select unnest(cast(:long_array as t_number_tbl))
select unnest(cast(:string_array as ntt_varchar))
```
В таком случае в качестве результатов запроса будет возвращена колонка со всевозможными значениями из данных
массивов, как если бы проводилась выборка из таблицы.

### Дополнительные правила переноса
Пока решено было не добавлять внешних ключей и партицирований в таблицы.
* ****

## Консольные клиенты { #cli-tools }

### Список таблиц { #show-tables }

**Postgres:**

```
\dt
\dt *.*
\dt public.*
\dt+  # как \dt, но с расширенной информацией по таблицам
select * from information_schema.tables where table_schema = 'public';
select * from pg_tables where schemaname='public';
```

`\dt` и `\dt+` понимают регулярные выражения, короткое описание см. <https://stackoverflow.com/a/15644918/2731799>


**MySQL:**

`show tables`

**Oracle:**

`select table_name from all_tables;`

### С какой схемой работаем { #use }

**Postgres:**

```
SET search_path = market_billing, shops_web, public;
```

После такого запроса каждая таблица из запроса, указанная без схемы, ищется в схемах из `search_path`.
Можно не устанавливать `search_path`, а всегда указывать таблицы в формате `schema.table` (например, `market_billing.bank_order`).

Можно записать нужный `search_path` в файл `~/.psqlrc`:
```
$ cat ~/.psqlrc
SET search_path = market_billing, shops_web, public;
```

**MySQL:**

```
use my_database;
```

Ведет себя аналогично postgres-овому `SET search_path = my_database`. Указать несколько database для поиска таблиц нельзя.

**Oracle:**

???

### Show create table { #show-table-ddl }

**Postgres:**

* <https://stackoverflow.com/questions/2593803/how-to-generate-the-create-table-sql-statement-for-an-existing-table-in-postgr>
* <https://serverfault.com/questions/231952/is-there-an-equivalent-of-mysqls-show-create-table-in-postgres>

**MySQL:**

```
desc my_table;
show create table my_table;
```

**Oracle:**

* <https://stackoverflow.com/questions/18264584/show-create-table-equivalent-in-oracle-sql>
* <https://stackoverflow.com/questions/35171093/how-to-get-comments-for-table-column-from-oracle-db-from-its-metadata>


### Заготовка описания { #template }

**Postgres:**

**MySQL:**

**Oracle:**

