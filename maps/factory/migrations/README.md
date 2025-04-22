This directory contains database migrations for projects:
- mapsfactory
- mapsfactory_signals

Database migrations are managed with pgmigrate_helper. See detailed instructions in pgmigrate_helper [README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/pgmigrate_helper/README.md).


## To create new migration
Just add file `V<version>__<description>.sql` to `migrations` subdirectory of corresponding project and run tests `ya make -ttt`.

## To build pgmigrate_helper
```
$ ya make pgmigrate_helper
```

## To check current migration version
```
$ ./pgmigrate_helper/pgmigrate_helper  -c config.yaml -e $ENV info

```
Where `$ENV` is one of: development, testing, stable (see config.yaml), and
${PROJECT} is one of `mapsfactory`, `mapsfactory_signals`.

## To install migration
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV  -t $VERSION migrate
```
where `$VERSION` is identifier of target migration version or `latest` (to install all available migrations).

