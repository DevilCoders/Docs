Database migrations are managed with pgmigrate_helper. See detailed instructions in pgmigrate_helper [README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/pgmigrate_helper/README.md).

## To create new migration
Just add file `V<version>__<description>.sql` to `migrations` directory and run tests `ya make -ttt`.

## To build pgmigrate_helper
```
$ ya make pgmigrate_helper
```

## To check current migration version
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV info

```
Where `$ENV` is one of: testing, load, stable (see config.yaml).

### stable
```
$ for i in `seq 0 7`; do echo stable_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e stable_$i info ; done 
```

### testing
```
$ for i in `seq 0 7`; do echo testing_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e testing_$i info ; done 
```

### load
```
$ for i in `seq 0 7`; do echo load_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e load_$i info ; done 
```

## To install migration
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV  -t $VERSION migrate
```
where `$VERSION` is identifier of target migration version or `latest` (to install all available migrations).

### stable
```
$ for i in `seq 0 7`; do echo stable_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e stable_$i -t latest migrate ; done 
```

### testing
```
$ for i in `seq 0 7`; do echo testing_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e testing_$i -t latest migrate ; done 
```

### load
```
$ for i in `seq 0 7`; do echo load_$i:; ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e load_$i -t latest migrate ; done 
```

