Database migrations are managed with [pgmigrate](https://github.com/yandex/pgmigrate/blob/master/doc/tutorial.md)


## Migration files
Migration files must be located in `migrations` directory and migration file names must follow the pattern `V<version>__<description>.sql`.
By default `migration` directory is assumed at path `.`. This path can be overriden by `-d` option.


## To check current migration version

```
ya make
./pgmigrate_helper -c ${CONFIG_PATH} -e ${ENV} info

```

Where `$ENV` is one of the environments specified in configuration file `$CONFIG_PATH`.
See example configuration file in example_config.yaml.

Example output:
```(json)
{
    "124": {
        "version": 124,
        "description": "Forced baseline",
        "type": "manual",
        "installed_by": "mapspro",
        "installed_on": "2020-04-30 20:23:27",
        "transactional": true
    },
    "125": {
        "version": 125,
        "description": "eye recognition postgresql upgrade",
        "type": "auto",
        "installed_by": "mapspro",
        "installed_on": "2020-04-30 20:23:56",
        "transactional": true
    },
    "126": {
        "version": 126,
        "type": "auto",
        "installed_by": null,
        "installed_on": null,
        "description": "traffic light toloka table postgresql upgrade",
        "transactional": true
    }
}
```


## To install migration
```
./bin/pgmigrate_helper -c $CONFIG_PATH -e development  -t $VERSION migrate
```
where `$VERSION` is identifier of target migration version or `latest` (to install all available migrations).


## Migrating to pgmigrate from other migration tool
Let's suppose that you already have a database with schema on version 3. But you have already reached this state without using pgmigrate. How should you migrate to version 4 and so on with it?

```
./bin/pgmigrate_helper -c $CONFIG_PATH -e $ENV -b 3 baseline
```
