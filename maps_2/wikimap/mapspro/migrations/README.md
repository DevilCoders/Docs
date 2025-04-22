Database migrations are managed with pgmigrate_helper. See detailed instructions in pgmigrate_helper [README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/pgmigrate_helper/README.md).

## To create new migration
Just add file `V<version>__<description>.sql` to `migrations` directory and run tests `ya make -tt`.

### Nontransactional migrations
Some postgresql statements cannot be executed under transaction. Such cases include but not limited to `CREATE INDEX CONCURRENTLY`, `ALTER TYPE ... ADD VALUE`. If you need these statements in your migration, you should mark the migration as nontransactional by naming it according to the pattern `V<version>__NONTRANSACTIONAL_<description>.sql`.

### Creating heavy indices
TL;DR: use `CREATE INDEX CONCURRENTLY IF NOT EXISTS ... ` in a nontransactional migration.

Sometimes you may need to create new index on some large portion of data. Doing it synchronously (`CREATE INDEX ...`) acquires exclusive lock on writing to the table and therefore may lead to a significant read-only time span. In production environment this is almost always unacceptable, so you should create such indices `CONCURRENTLY` and mark migration as NONTRANSACTIONAL. Keep in mind that nontransactional index creation will not be rolled back in case of error, so it is better to keep `IF NOT EXISTS` parameter to prevent double index creation as it will explicitly alert you that something is wrong.

### What can go wrong
You should still be concerned about `ShareUpdateExclusiveLock` that is acquired in case of creating an index concurrently, as it still may fail due to lock timeout - a lock of this type is also acquired when postgres performs vacuum on the same table (the most common case). One way to mitigate this is to extend lock timeout explicitly in the migration, another one is retrying to apply the failed migration (possibly with cleaning up invalid index).

Once concurrent index creation failed, you should check if actual attempt did take place. Use this query:
```
SELECT * FROM pg_class, pg_index WHERE pg_index.indisvalid = false AND pg_index.indexrelid = pg_class.oid;
```
Drop invalid index, check with `\d+ schema.table` if index does not exist and try again. `IF NOT EXISTS` parameter helps greatly here.

Do not forget to mark your migration as NONTRANSACTIONAL and run tests.

## To build pgmigrate_helper
```
$ ya make pgmigrate_helper
```

## To check current migration version
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV info

```
Where `$ENV` is one of: development, testing, stable (see config.yaml).

## To install migration
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV  -t $VERSION migrate
```
where `$VERSION` is identifier of target migration version or `latest` (to install all available migrations).
