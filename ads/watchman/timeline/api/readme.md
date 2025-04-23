## Testing
Run only unit tests
```
~/arcadia/ads/watchman/timeline/api/tests/ut$ ya make -t .
```
For running fat and integration tests you need install PostgreSQL on linux machine
(you can't build binary for fat tests on MacOS currently)

```
~/arcadia/ads/watchman/timeline/api/tests$ ya make -ttt .
```


## Migrations

Migrations order is based on current applied migrations on test server.

To generate migration type.

```bash
~/arcadia/ads/watchman/timeline/api/docker$ POSTGRES_USER=<user> POSTGRES_PASSWORD=<password> make generate-migration MSG=<commit message>
```

Migration will appear here:
```
~/arcadia/ads/watchman/timeline/api/migrations/alembic/versions$ ls
...
2018-01-26T23-57_8438bda6dbe2_initial_tables.py
2018-01-28T22-04_48e6c0f4bce4_rename_timeline_table.py
...
```
Ensure that your newly created migration is correct, either rewrite it manually. Then commit it with other code.

## Update holidays for long period

Choose APP_CONFIG_NAME for production and staging database.
```bash
~/arcadia/ads/watchman/timeline/api/bin/calendar_service_manager$ POSTGRES_USER=<user> POSTGRES_PASSWORD=<password> APP_CONFIG_NAME=staging ./calendar_service_manager --start=2017-01-01 --end=2018-01-01
```

## Update slices enums

Choose APP_CONFIG_NAME for production and staging database.
```bash
~/arcadia/ads/watchman/timeline/api/bin/timeline_db_manager$ POSTGRES_USER=<user> POSTGRES_PASSWORD=<password> APP_CONFIG_NAME=staging ./timeline_db_manager sync_enums --path ../../resources
```
