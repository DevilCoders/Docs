## yamail-copy-user - копирование данных

    $ yamail-copy-user --from_db=oracle:ymail/ympass@mdb302 --to_db=postgre:dbname=maildb --from_id=42 --to_id=52 -e local --force

`--from_id`, `--to_id` - для для `oracle` это `suid`, для `pg` `uid`


## инциализация sharddb

Нужен [pgmigrate](https://github.yandex-team.ru/secwall/pgmigrate)

    ~/src/pg/sharddb salt $ pwd
    /home/wizard/src/pg/sharddb
    $ psql
    wizard=# CREATE DATABASE sharddb;
    CREATE DATABASE
    wizard=# CREATE USER sharpei PASSWORD 'sharpeipass';
    wizard=# \q
    $ ls -l migrations/
    total 8
    -rw-rw-r-- 1 wizard wizard 706 Jun 22 16:20 V1__Initial.sql
    -rw-rw-r-- 1 wizard wizard 519 Jun 22 16:20 V2__transfer.sql
    pgmigrate t2 -d. -c 'dbname=sharddb' -a afterAll:grants migrate
    creating type schema_version_type CREATE TYPE creating table schema_version CREATE TABLE
    Migrating to version 1
    Migrating to version 2
    Executing afterAll callbacks:
    grants/sharpei.sql


## ipv6-only && pip
Текущий Pypi не умеет `ipv6`.

 * запускать `pip` с указанием индекса.

        pip install -i https://pypi.yandex-team.ru/simple/

 * добавить `index-url` в `/etc/pip.conf` или `~/.pip.conf`

 		[global]
		index-url = https://pypi.yandex-team.ru/simple/

