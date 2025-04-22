# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

For running the local database server, applying migrations and connecting to a db cluster with a cli database client
you will need [docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/) installed.

You should login to the [yandex docker registry](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
in order to be able pull and push images.

For deploying to the testing and production app clusters you will need to setup [ya](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup)
and get a token for using [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools#authorization) .

The ya tool is also used for downloading the project's secrets.

[jq](https://stedolan.github.io/jq/) utility tool is also used in some development scripts, so you'll need to have it installed.

## Getting Started

1. Go to the service folder in Arcadia

   ```sh
   cd /maps/front/services/parking-int
   ```

2. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

3. Install dependencies and setup database for local development
   ```sh
    make deps
    make dev.secrets
    make db.set-local-env
    make db.local-reset
   ```

4. Run server in development mode

    ```sh
    make build-watch
    MAPS_NODEJS_PORT=8666 make dev # optionally override port
    ```

## Testing

For run all api tests use the command:

```sh
make validate
```

For run manual tests to check providers api use the command:

```sh
make run-test-manual
```

For some of the manual tests an ssh-tunnel is required. For example to run the manual tests for MTS bank:
```sh
make ssh-tunnel

# in another terminal run
MOCHA_OPTIONS="--timeout 1200000 --grep mts" make run-test-manua
```

## Connect to the database
To connect to the local database server with psql simply run:
```sh
make db.connect
```

For connecting to other environments use the `DB_ENV` variable

For production
```sh
make db.connect DB_ENV=testing
```

### Running tests for migrations changes

If you're changing a migration file (`/db/migrations/*`) you will need a clean version of the DB, so that your changed
migration is applied. You can do this by stopping the container with the local DBMS before running the tests:
```sh
make db.local-stop test
```

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools) to interface with docker, the
docker registry and the cloud platform Yandex Deploy.

### Release to testing

```sh
make patch # or minor, major
arc pr create --push --publish --no-edit
```
Merge new PR after all checks. Pull trunk. Then create and push tag to `tags/releases`:
```sh
make arc-tag
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
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

## Load testing

### Step 1. Create PostgreSQL cluster in MDB Junk

* Install [Terraform CLI](https://www.terraform.io/downloads).
* Get Yandex Cloud [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=8cdb2f6a0dca48398c6880312ee2f78d) and export it as `TF_VAR_yc_token` environment variable.
* Run `stress-db-create-cluster` make target.

```sh
export TF_VAR_yc_token=<token>
make stress-db-create-cluster
```

### Step 2. Apply DB migrations to the newly created cluster

* After the cluster is created, run `make stress-db-hosts` to see the list of DB cluster hosts.
* Copy these hosts into the `db.hosts` option of the `stress` environment config in [config.ts](./src/app/config.ts).
* Now you can apply the migrations for `stress` environment:

```sh
# Dry run
make db.migrate DB_ENV=stress

# Apply migrations if everything is okay
make db.migrate DB_ENV=stress DB_MIGRATE_DRY_RUN=0
```

### Step 3. Deploy the stress stage and shoot

Because we modified the `config.ts` file, we'll need to build a new Docker image with these changes. Modify [.qtools.json](./.qtools.json) by appending a custom suffix to `registry.tag`. You can use `-{yourusername}-stress` suffix, for example `0.0.27-yesenarman-stress`.

Now deploy the stress stage and start the shooting:

```sh
qtools release stress --force --wait

# Wait for the deployment to finish...

# Fire!
make stress-fire
```

We use a custom [fire.ts](./src/tools/stress/fire.ts) script, because there are some options in the Yandex Tank config that we need to override before shooting.

### Step 4. Clean up

When you are done with shooting, use `stress-clean` target to destroy the DB cluster and the stress deploy stage.

```sh
make stress-clean
```

## Troubleshooting

### make db.* errors
You can encounter errors while running any make target related to the database (`make db.migrate`). For example:
```sh
ERROR: for db  Cannot start service db: error while creating mount source path '/home/dodev/code/arcadia/maps/front/services/parking-int/db/create-extensions.sql': mkdir /home/dodev/code/arcadia: file exists
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
Makefile:4: *** missing separator.  Stop.
```
you should get a fresh version of make through `brew install make`.
The error is caused by the `undefine` keyword which is not available in the macOS default version of make.
Don't forget to add `export PATH="/usr/local/opt/make/libexec/gnubin:$PATH"` in `.bashrc` to use new version of make

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

### How to get Debug User Tickets for local development

1. Run `make build dev` to start the app and the tvmtool daemon.
2. Get an [OAuth token](https://oauth.yandex.ru/authorize?response_type=token&client_id=be4044964e7243f4b6dd1b6785e78cd3) and export it as `DEBUG_USER_TICKETS_TOKEN` environment variable:
```sh
export DEBUG_USER_TICKETS_TOKEN=<token>
```
3. To get a user ticket and print it to stdout, run:
```sh
make dev.get-debug-user-ticket
```
4. Or you can use it together with `curl` like this:
```sh
curl -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" "http://localhost:8080/v1/check_balance?provider=mos"
```

## Sending requests

### Parking flow
1. Get active parking sessions:
```sh
curl "localhost:8080/v1/get_active_parking_sessions" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)"
```
2. Check balance:
```sh
curl "localhost:8080/v1/check_balance?provider=mos" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)"
```
3. Check price for parking zone:
   * for a new session:
   ```sh
   curl "localhost:8080/v1/check_price?provider=mos&providerParkingId=3121&durationMinutes=60" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)"
   ```
   * for extend an existing session:
   ```sh
   curl "localhost:8080/v1/check_price?provider=mos&providerParkingId=3121&durationMinutes=30&sessionId=<session_public_id>" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)"
   ```
4. Topup balance. Two ways:
   * Use payment flow
   * Use devtools router:
   ```sh
   curl -X POST "localhost:8080/v1/devtools/topup_mos_balance" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" -d '{"amount":"10"}'
   ```
5. Start parking:
```sh
curl "localhost:8080/v1/start_parking_session" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" -d '{"provider":"mos", "providerParkingId":"3121","durationMinutes":"30","vehiclePlate":"A101AA11","appId":"ru.yandex.yandexmaps.debug"}'
```
4. Extend parking:
```sh
curl "localhost:8080/v1/extend_parking_session" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" -d '{"provider":"mos","durationMinutes":"30","sessionId":"<session_public_id>"}'
```
5. Stop parking:
```sh
curl "localhost:8080/v1/stop_parking_session" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" -d '{"provider":"mos","sessionId":"<session_public_id>"}'
```

### Create local payment

1. Create ssh-tunnel for requests to multicarta:
```sh
make ssh-tunnel
```
2. Initiate payment:
```sh
curl "localhost:8080/v1/initiate_payment" -H "Content-Type: application/json" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" -d '{"provider":"mos","amount":"1","type":"PAYMENT_FORM","payload":{"source":"navi","lang":"ru"}}'
```
3. Enter card credentials, use data from last page in the [document](https://st.yandex-team.ru/MAPSHTTPAPI-2382#6144665dce67fc70167d042c)
4. Get `paymentId` from url after redirect
5. Check payment status and topup parking balance:
```sh
curl "localhost:8080/v1/check_payment_status?provider=mos&payment_id=<payment id from previous step>" -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)"
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
