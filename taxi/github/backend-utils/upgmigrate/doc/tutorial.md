# µPGmigrate tutorial

We'll play around with an example database `testdb`. We will use a `dummy` user to own the database and carry out the migrations and we will grant readonly rights to user `taxiro`. We will create two 'logical' shards in the database and they will share datatype definitions.

## Base directory structure of our example

Our [Example db](testdb) migrations dir structure looks like this:
```bash
testdb
├── callbacks           # directory with sql callbacks
│   ├── afterAll        # will be executed before commit and after last migration
│   ├── afterEach       # will be executed after each migration
│   ├── beforeAll       # will be executed after begin and before first migration
│   └── beforeEach      # will be executed before each migration
├── grants              # use this dir to set special callbacks for grants
├── migrations          # shard migrations dir
├── types               # database user datatypes shared between shards
├── datatypes.yml       # configuration for data types common for all 'logical' shards
├── migrations.yml      # shard-migrate shard configuration
├── create_testdb.sql   # script to create the dummy user and test database
```
Every sql file has special operation on table `public.ops`.
This will help in understanding what is going on in each `shard-migrate` run.

## Migration file name pattern

All migration files should have versions and names in the following format
```
V<version>__<description>.sql
          ^^ note the two underscores
```
Note: files not matching this pattern will be skipped.

## Creating users and `testdb`

We'll need a dummy user and a database for our experiments. Execute the following statements in `psql` console:
```
postgres=# CREATE ROLE dummy WITH LOGIN PASSWORD 'dummy';
CREATE ROLE
postgres=# CREATE ROLE taxiro WITH LOGIN PASSWORD 'taxiro';
CREATE ROLE
postgres=# CREATE DATABASE testdb;
CREATE DATABASE
postgres=# ALTER DATABASE testdb OWNER TO dummy;
```
 or just use the [script](testdb/create_testdb.sql)
 ```bash
user@localhost testdb $ psql -f create_testdb.sql 
 ```

## Getting migrations info before first migration

There are two major parts in our deployment, the shared datatypes and 'logical' shards. First we will have a look at the datatypes.

```bash
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml info
{
    "1": {
        "installed_by": null,
        "version": 1,
        "description": "initial datatypes",
        "transactional": true,
        "type": "auto",
        "installed_on": null
    }
}
```

Now we will look at our logical shards
```bash
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -t 1 info; done
Shard dummy_0
{
    "1": {
        "version": 1,
        "type": "auto",
        "installed_on": null,
        "installed_by": null,
        "description": "Initial schema",
        "transactional": true
    }
}
Shard dummy_1
{
    "1": {
        "type": "auto",
        "version": 1,
        "installed_by": null,
        "installed_on": null,
        "description": "Initial schema",
        "transactional": true
    }
}
```
Here we see json description of migrations that will be applied if we want to get to version 1.

```bash
user@localhost testdb $ ../../shard-migrate.py -t 1 info
{
    "1": {
        "description": "Initial schema dummy",
        "transactional": true,
        "version": 1,
        "installed_by": null,
        "type": "auto",
        "installed_on": null
    }
}
```
Here we see json description of migrations that will be applied if we want to get to version 1.

Let's try to check steps to apply up to version 3 but ignoring version 1:
```bash
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -b 1 -t 3 info; done
Shard dummy_0
{
    "2": {
        "description": "Add baz column to foo",
        "version": 2,
        "transactional": true,
        "installed_on": null,
        "type": "auto",
        "installed_by": null
    },
    "3": {
        "description": "NONTRANSACTIONAL Add index on baz column",
        "version": 3,
        "transactional": false,
        "installed_on": null,
        "type": "auto",
        "installed_by": null
    }
}
Shard dummy_1
{
    "2": {
        "installed_on": null,
        "version": 2,
        "installed_by": null,
        "description": "Add baz column to foo",
        "transactional": true,
        "type": "auto"
    },
    "3": {
        "installed_on": null,
        "version": 3,
        "installed_by": null,
        "description": "NONTRANSACTIONAL Add index on baz column",
        "transactional": false,
        "type": "auto"
    }
}
```

## Migrating to first version

We will migrate the shared datatypes to version 1 and then apply version 1 to only one of our 'logical' shards.

```bash
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml -t 1 migrate
user@localhost testdb $ echo $?
0
user@localhost testdb $ ../../shard-migrate.py -i dummy_0 -t 1 migrate
user@localhost testdb $ echo $?
0
```
Ok. Migration applied. Now let's check the migration info again
```bash
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml -t 1 info
{
    "1": {
        "installed_on": "2019-07-11 14:21:28",
        "transactional": true,
        "installed_by": "dummy",
        "description": "initial datatypes",
        "type": "auto",
        "version": 1
    }
}
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -t 1 info; done
Shard dummy_0
{
    "1": {
        "transactional": true,
        "version": 1,
        "installed_on": "2019-07-11 14:23:02",
        "type": "auto",
        "installed_by": "dummy",
        "description": "Initial schema"
    }
}
Shard dummy_1
{
    "1": {
        "installed_by": null,
        "type": "auto",
        "description": "Initial schema",
        "version": 1,
        "installed_on": null,
        "transactional": true
    }
}
```

You can see that the shard dummy_1 wasn't yet installed.

Let's see what is in our db now.

```bash
user@localhost testdb $ psql testdb
psql (10.5)
Type "help" for help.

testdb=# SELECT * FROM ops;
 seq | schema  |                   op
-----+---------+-----------------------------------------
   1 | dummy   | beforeAll 00_create_database_ops.sql
   2 | dummy   | grants on dummy schema
   3 | dummy_0 | beforeAll 00_create_database_ops.sql
   4 | dummy_0 | beforeEach 00_dummy_before_each.sql
   5 | dummy_0 | migration V0001__Initial_schema_foo.sql
   6 | dummy_0 | afterEach 00_dummy_after_each.sql
   7 | dummy_0 | afterAll 00_dummy_after_all.sql
   8 | dummy_0 | grants on dummy_0 schema
(8 rows)

testdb=# \dt dummy.dummy
        List of relations
 Schema  | Name  | Type  | Owner
---------+-------+-------+-------
 dummy_0 | dummy | table | dummy
(1 row)

testdb=# \dS+ dummy*.dummy
                                       Table "dummy_0.dummy"
 Column |      Type       | Collation | Nullable | Default | Storage  | Stats target | Description
--------+-----------------+-----------+----------+---------+----------+--------------+-------------
 id     | bigint          |           | not null |         | plain    |              |
 bar    | dummy.test_type |           | not null |         | extended |              |
Indexes:
    "dummy_pkey" PRIMARY KEY, btree (id)
```

Let's check if `taxiro` user can really do something with our new table.
```bash
psql "dbname=testdb user=taxiro password=taxiro host=localhost"
psql (10.5)
Type "help" for help.

testdb=> SELECT * FROM dummy_0.dummy;
 id | bar
----+-----
(0 rows)
```

## Mixing transactional and nontransactional migrations
Let's try to go to version 3.
```
user@localhost testdb $ ../../shard-migrate.py -i dummy_0 -t 3 migrate
2019-07-11 15:02:53,218 ERROR   : Unable to mix transactional and nontransactional migrations
Traceback (most recent call last):
  File "../../shard-migrate.py", line 860, in <module>
    _main()
  File "../../shard-migrate.py", line 856, in _main
    COMMANDS[args.cmd](config)
  File "../../shard-migrate.py", line 688, in migrate
    raise MigrateError('Unable to mix transactional and '
__main__.MigrateError: Unable to mix transactional and nontransactional migrations
```
Oops! It complained. But why? The main reason for this is quite simple:
Your production databases are likely larger than test ones.
And migration to version 3 could take a lot of time.
You definitely should stop on version 2, check that everything is working fine,
and then move to version 3.

## Migrating to second version
Ok. Now let's try version 2 and apply it to our both 'shards'.
```bash
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -t 2 migrate; done
Shard dummy_0
Shard dummy_1
user@localhost testdb $ echo $?
0
```
Looks good. But what is in db?
```
user@localhost testdb $ psql testdb
psql (10.5)
Type "help" for help.

testdb=# SELECT * FROM ops;
  seq | schema  |                     op
-----+---------+--------------------------------------------
   1 | dummy   | beforeAll 00_create_database_ops.sql
   2 | dummy   | grants on dummy schema
   3 | dummy_0 | beforeAll 00_create_database_ops.sql
   4 | dummy_0 | beforeEach 00_dummy_before_each.sql
   5 | dummy_0 | migration V0001__Initial_schema_foo.sql
   6 | dummy_0 | afterEach 00_dummy_after_each.sql
   7 | dummy_0 | afterAll 00_dummy_after_all.sql
   8 | dummy_0 | grants on dummy_0 schema
   9 | dummy_0 | beforeAll 00_create_database_ops.sql
  10 | dummy_0 | beforeEach 00_dummy_before_each.sql
  11 | dummy_0 | migration V0002__Add_baz_column_to_foo.sql
  12 | dummy_0 | afterEach 00_dummy_after_each.sql
  13 | dummy_0 | afterAll 00_dummy_after_all.sql
  14 | dummy_0 | grants on dummy_0 schema
  15 | dummy_1 | beforeAll 00_create_database_ops.sql
  16 | dummy_1 | beforeEach 00_dummy_before_each.sql
  17 | dummy_1 | migration V0001__Initial_schema_foo.sql
  18 | dummy_1 | afterEach 00_dummy_after_each.sql
  19 | dummy_1 | beforeEach 00_dummy_before_each.sql
  20 | dummy_1 | migration V0002__Add_baz_column_to_foo.sql
  21 | dummy_1 | afterEach 00_dummy_after_each.sql
  22 | dummy_1 | afterAll 00_dummy_after_all.sql
  23 | dummy_1 | grants on dummy_1 schema
(23 rows)

testdb=# \dS+ dummy*.dummy
                                                  Table "dummy_0.dummy"
      Column      |      Type       | Collation | Nullable |       Default        | Storage  | Stats target | Description
------------------+-----------------+-----------+----------+----------------------+----------+--------------+-------------
 id               | bigint          |           | not null |                      | plain    |              |
 bar              | dummy.test_type |           | not null |                      | extended |              |
 alternate_colour | dummy.rainbow   |           | not null | 'red'::dummy.rainbow | plain    |              |
Indexes:
    "dummy_pkey" PRIMARY KEY, btree (id)

                                                  Table "dummy_1.dummy"
      Column      |      Type       | Collation | Nullable |       Default        | Storage  | Stats target | Description
------------------+-----------------+-----------+----------+----------------------+----------+--------------+-------------
 id               | bigint          |           | not null |                      | plain    |              |
 bar              | dummy.test_type |           | not null |                      | extended |              |
 alternate_colour | dummy.rainbow   |           | not null | 'red'::dummy.rainbow | plain    |              |
Indexes:
    "dummy_pkey" PRIMARY KEY, btree (id)

```
As we can see migration steps are almost the same as in version 1 and they were also applied to the second shard.

## Migrating to version 3 with nontransactional migration
```
user@localhost testdb $ ../../shard-migrate.py -t 3 migrate
user@localhost testdb $ echo $?
0
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -t 3 migrate; done
user@localhost testdb $ echo $?
0
```

In database:
```
user@localhost testdb $ psql testdb
psql (9.5.4)
Type "help" for help.

testdb=# SELECT * FROM ops;
 seq | schema  |                              op
-----+---------+---------------------------------------------------------------
   1 | dummy   | beforeAll 00_create_database_ops.sql
   2 | dummy   | grants on dummy schema
   3 | dummy_0 | beforeAll 00_create_database_ops.sql
   4 | dummy_0 | beforeEach 00_dummy_before_each.sql
   5 | dummy_0 | migration V0001__Initial_schema_foo.sql
   6 | dummy_0 | afterEach 00_dummy_after_each.sql
   7 | dummy_0 | afterAll 00_dummy_after_all.sql
   8 | dummy_0 | grants on dummy_0 schema
   9 | dummy_0 | beforeAll 00_create_database_ops.sql
  10 | dummy_0 | beforeEach 00_dummy_before_each.sql
  11 | dummy_0 | migration V0002__Add_baz_column_to_foo.sql
  12 | dummy_0 | afterEach 00_dummy_after_each.sql
  13 | dummy_0 | afterAll 00_dummy_after_all.sql
  14 | dummy_0 | grants on dummy_0 schema
  15 | dummy_1 | beforeAll 00_create_database_ops.sql
  16 | dummy_1 | beforeEach 00_dummy_before_each.sql
  17 | dummy_1 | migration V0001__Initial_schema_foo.sql
  18 | dummy_1 | afterEach 00_dummy_after_each.sql
  19 | dummy_1 | beforeEach 00_dummy_before_each.sql
  20 | dummy_1 | migration V0002__Add_baz_column_to_foo.sql
  21 | dummy_1 | afterEach 00_dummy_after_each.sql
  22 | dummy_1 | afterAll 00_dummy_after_all.sql
  23 | dummy_1 | grants on dummy_1 schema
  24 | dummy   | migration V0003__NONTRANSACTIONAL_Add_some_colors.sql
  25 | dummy_0 | migration V0003__NONTRANSACTIONAL_Add_index_on_bar_column.sql
  26 | dummy_1 | migration V0003__NONTRANSACTIONAL_Add_index_on_bar_column.sql
(26 rows)

testdb=# \dS+ dummy*.dummy
                                                  Table "dummy_0.dummy"
      Column      |      Type       | Collation | Nullable |       Default        | Storage  | Stats target | Description
------------------+-----------------+-----------+----------+----------------------+----------+--------------+-------------
 id               | bigint          |           | not null |                      | plain    |              |
 bar              | dummy.test_type |           | not null |                      | extended |              |
 alternate_colour | dummy.rainbow   |           | not null | 'red'::dummy.rainbow | plain    |              |
Indexes:
    "dummy_pkey" PRIMARY KEY, btree (id)
    "i_dummy_bar" btree (bar)

                                                  Table "dummy_1.dummy"
      Column      |      Type       | Collation | Nullable |       Default        | Storage  | Stats target | Description
------------------+-----------------+-----------+----------+----------------------+----------+--------------+-------------
 id               | bigint          |           | not null |                      | plain    |              |
 bar              | dummy.test_type |           | not null |                      | extended |              |
 alternate_colour | dummy.rainbow   |           | not null | 'red'::dummy.rainbow | plain    |              |
Indexes:
    "dummy_pkey" PRIMARY KEY, btree (id)
    "i_dummy_bar" btree (bar)
```
No callbacks were applied this time (we are trying to run the absolute
minimum of operations outside of transactions).

## Baseline

Let's suppose that you already have a database with schema on version 3.
But you have already reached this state without using `shard-migrate.py`.
How should you migrate to version 4 and so on with it?

Let's remove schema_version info from our database
```
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml clean
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i clean; done
Shard dummy_0
Shard dummy_1
```

Now let's check how ../../shard-migrate.py will bring us to version 3:
```
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml -t 3 info
{
    "1": {
        "type": "auto",
        "transactional": true,
        "version": 1,
        "installed_by": null,
        "installed_on": null,
        "description": "Initial datatypes"
    },
    "3": {
        "type": "auto",
        "transactional": false,
        "version": 3,
        "installed_by": null,
        "installed_on": null,
        "description": "NONTRANSACTIONAL add some colors"
    }
}
```
This looks really bad. Our migration v1 will definitely fail (because datatypes already exist). Let's tell `shard-migrate.py` that our database is already on version 3.
```
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml -b 3 baseline
user@localhost testdb $ for i in `seq 0 1`; do echo "Shard dummy_$i"; ../../shard-migrate.py -i dummy_$i -b 3 baseline; done
Shard dummy_0
Shard dummy_1
user@localhost testdb $ ../../shard-migrate.py -f datatypes.yml -t 3 info
{
    "3": {
        "installed_by": "dummy",
        "description": "Forced baseline",
        "installed_on": "2019-07-11 16:24:38",
        "transactional": true,
        "version": 3,
        "type": "manual"
    }
}
```

## Migrations on empty database

When you have hundreds of migrations with some nontransactional ones
you really don't want to stop on each of them to get your empty database
to specific version (consider creating new database for some experiments).

../../shard-migrate.py is able to run such kind of migration in single command run
(but you should definitely know what are you doing).

Let's try it.
Drop and create empty `testdb`
```
postgres=# DROP DATABASE testdb;
DROP DATABASE
postgres=# CREATE DATABASE testdb;
CREATE DATABASE
```

Now migrate to latest available version
```
user@localhost testdb $ ../../shard-migrate.py -t latest migrate
```

Operations log will look like this:
```
user@localhost testdb $ psql testdb
psql (10.5)
Type "help" for help.

 seq | schema  |                              op
-----+---------+---------------------------------------------------------------
   1 | dummy   | beforeAll 00_create_database_ops.sql
   2 | dummy   | grants on dummy schema
   3 | dummy   | migration V0003__NONTRANSACTIONAL_Add_some_colors.sql
   4 | dummy_0 | beforeAll 00_create_database_ops.sql
   5 | dummy_0 | beforeEach 00_dummy_before_each.sql
   6 | dummy_0 | migration V0001__Initial_schema_foo.sql
   7 | dummy_0 | afterEach 00_dummy_after_each.sql
   8 | dummy_0 | beforeEach 00_dummy_before_each.sql
   9 | dummy_0 | migration V0002__Add_baz_column_to_foo.sql
  10 | dummy_0 | afterEach 00_dummy_after_each.sql
  11 | dummy_0 | afterAll 00_dummy_after_all.sql
  12 | dummy_0 | grants on dummy_0 schema
  13 | dummy_0 | migration V0003__NONTRANSACTIONAL_Add_index_on_bar_column.sql
  14 | dummy_1 | beforeAll 00_create_database_ops.sql
  15 | dummy_1 | beforeEach 00_dummy_before_each.sql
  16 | dummy_1 | migration V0001__Initial_schema_foo.sql
  17 | dummy_1 | afterEach 00_dummy_after_each.sql
  18 | dummy_1 | beforeEach 00_dummy_before_each.sql
  19 | dummy_1 | migration V0002__Add_baz_column_to_foo.sql
  20 | dummy_1 | afterEach 00_dummy_after_each.sql
  21 | dummy_1 | afterAll 00_dummy_after_all.sql
  22 | dummy_1 | grants on dummy_1 schema
  23 | dummy_1 | migration V0003__NONTRANSACTIONAL_Add_index_on_bar_column.sql
(23 rows)
```

