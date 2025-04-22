# `mmm` - Microservice Maintainer Multitool

In form of common Makefile targets.

See usage: [https://a.yandex-team.ru/search?search=tools/mmm](https://a.yandex-team.ru/search?search=tools%2Fmmm,%5Emaps%2Ffront%2Fservices%2F.*Makefile,C,arcadia,,200&repo=arcadia)

## Installation

1. Include `mmm` at the top of `Makefile`:
```Makefile
# mmm-config-dev.https-enable := 1 (optionally enable something)
-include ../../tools/mmm/mmm.mk
ci.postinstall: # Dummy target
```

(copy line with `ci.postinstall` as is)

2. Add postinstall script to `package.json`: `"scripts": {"postinstall": "make ci.postinstall"}` (needed by CI)
3. Add `unsafe-perm = true` to `.npmrc` (needed by CI)

## Environment

`mmm` autmatically sets:
- `MAPS_STAGE`
- `MAPS_NODEJS_PORT`
- `TVMTOOL_LOCAL_AUTHTOKEN`
- `DEPLOY_TVM_TOOL_URL` (+ `MAPS_DEPLOY_TVM_TOOL_PORT` which is handy for integration tests)

## Targets

### `make dev.setup` - local environment with hosts and secrets

Downloads resources specified in from your `testing.yml` into `.dev/`.

```sh
make dev.hosts      # Downloads hosts
make dev.secrets    # Downloads secrets
make dev.domains    # Kindly asks you to update your /etc/hosts
make dev.https      # Generates certificates (optional, mmm-config-dev.https-enable)
make dev.uatraits   # Downloads uatraits (optional, mmm-config-dev.uatraits-enable)
make dev.geobase    # Downloads geobase (optional, mmm-config-dev.geobase-enable)
```

### `make version...` - versioning helpers

Optional, enable with `mmm-config-version-enable := 1`.

```sh
make version.major
make version.minor
make version.patch
make version.arc-tag
```

### `make dev.tunneler`

Runs tunneler for `MAPS_NODEJS_PORT`.

### `make db...` - work with database

```sh
make db.set-local-env              # Create files with the settings for local database
make db.connect DB_ENV=testing     # Сonnect to the database server with psql
make db.local-wait                 # Wait until it is possible to connect to the local database
make db.local-start                # Start the container with the local database
make db.local-stop                 # Stop the container with the local database
make db.local-logs                 # Show logs for local database
make db.local-reset                # Setup database for local development
make db.local-init-test-db         # Init the database for integration tests
```

### DB migrations
To migrate a DB cluster you can use:
```sh
make db.migrate
```

By default the migration is applied to the `development` environment. If you wish to target the testing environment for example,
set the `DB_ENV` variable to `testing`
```sh
make db.migrate DB_ENV=testing
```

Another defaultly set parameter is the dry-run flag. If you are sure you want to apply the migration pass `DB_MIGRATE_DRY_RUN=0`:

```sh
make db.migrate DB_MIGRATE_DRY_RUN=0
```

If needed a specific target revision of the migrations can applied using the `DB_MIGRATE_TARGET` variable:
```sh
make db.migrate DB_MIGRATE_TARGET=3
```
The default version is `latest`.

Let's say you want to apply version `3` of the schema to the `testing` cluster. You should type in:

```sh
make db.migrate DB_ENV=testing DB_MIGRATE_TARGET=3
# make sure there were no errors in the output
make db.migrate DB_ENV=testing DB_MIGRATE_TARGET=3 DB_MIGRATE_DRY_RUN=0
```

### Running tests for migrations changes

If you're changing a migration file (`/db/migrations/*`) you will need a clean version of the DB, so that your changed
migration is applied. You can do this by stopping the container with the local DBMS before running the tests:
```
make db.local-stop test
```

## Troubleshooting

### make db.* errors
You can encounter errors while running any make target related to the database (`make db.migrate`). For example:
```sh
ERROR: for db  Cannot start service db: error while creating mount source path ...
```
It means that `docker` cannot access the local fs and mount it in the container. The fix is to mount arcadia with the `--allow-other` flag:
```sh
arc mount --allow-other -m arcadia/ -S arcadia_store/
```
You will probably need to enable the `user_allow_other` feature in `/etc/fuse.conf` by uncommenting it.

Explanation: `arc` uses FUSE for mounting the whole arcadia repository locally and it mounts it with permissions for only the current user.
`docker` uses it's own user `docker` and it cannot access the fs parts mounted by `arc`. With allow other permissions for other users are
added to the files.

### macOS and make errors
If you're using macOS and when running any make target you encounter errors sucha as:
```
Makefile:126: *** missing separator.  Stop.
```
you should get a fresh version of make through `brew install make`.
The error is caused by the `undefine` keyword which is not available in the macOS default version of make.

### db.connect, macOS and MDB
If you're running `make db.connect` or `make db.migrate` on macOS and trying to target remote MDB clusters
you will encouter connection errors. This is because by default these targets are ran in docker containers
and docker on macOS cannot connect to IPV6-only hosts, such as the hosts of our PG clusters.

As a workaround, if you have `psql` and/or `pgmigrate` installed you can use them instead of the docker-packed
executables:
```sh
export PSQL_EXECUTABLE=psql
make db.connect DB_ENV=production # this will use the host machine psql instead of the docker-contained

export PGMIGRATE_EXECUTABLE=pgmigrate
make db.migrate DB_ENV=prodcution # the same is valid for pgmigrate
```

## Contributing

When updating `mmm` you need to update all services accordingly.
You can find all service using `mmm` by running `./lib/used-by` script.

```sh
while IFS=$'\t' read -r service folder; do
    ./lib/lint-usage "$service" "$folder"
done < <(./lib/used-by)
```
