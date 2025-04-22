Requrements
-----------

* sshfs
* libmagick++9
* python >= 2.5
* yandex-python-yutil
* python-sqlalchemy
* python-psycopg2
* libyandex-maps-tileutils-python
* python-webpy
* python-simplejson
* libyandex-maps-coordtrans-python
* yandex-lockf
* autoconf
* yandexcommon

Миграция базы
-------------

Создание новых скриптов для апгрейда/даунгрейда:

* scripts/db_migrate.py script_sql postgres
* пойти и поредактировать новые файлики в migrations/versions/*


Build requirements
------------------

* libmagick++9-dev
* swig
* python-dev >= 2.5

SQL creation
------------

To MySQL:

    zcat /opt/quoter/data/20090421/200_sat_1.8.0.dump.gz | ~/git/mapstat/inserter.py| mysql -u root world

To file:

    zcat /opt/quoter/data/20090421/200_sat_1.8.0.dump.gz | ~/git/mapstat/inserter.py > data.sql

Test request
------------

For MySQL

    SELECT COUNT(*) FROM tiles WHERE Contains(GeomFromText('POLYGON((633344 328704, 633472 328704, 633472 328832, 633344 328832, 633344 328704))'), tile);

For PostgreSQL:

    SELECT COUNT(*) FROM tiles WHERE ST_Contains(GeomFromText('POLYGON((633344 328704, 633472 328704, 633472 328832, 633344 328832, 633344 328704))', -1), tile);

    select ( SELECT SUM(counter) FROM tiles t2 WHERE ST_Contains(t1.tile, t2.tile) ), AsText(tile) from tiles t1 where scale=2;
    1m42.544s
