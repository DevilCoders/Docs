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

1. Switch to needed Node.js version from `.nvmrc` file:

    ```sh
    nvm use
    ```

2. Install dependencies and setup database for local development

    ```sh
    make deps
    make db-local-reset
    ```

3. Add secrets for local development

    ```sh
    make secrets
    ```

4. Run server in development mode

    ```sh
    make build-watch
    MAPS_NODEJS_PORT=8666 make dev # optionally override port
    ```

By default http-service starts listening on port `8080`. If you started the application locally it
should respond on http://localhost:8080/ping

In order to be able to send requests to the launched app you need to generate dev-time TVM tickets and pass them to the `x-ya-service-ticket` (for each endpoint) and `x-ya-user-ticket` (for non-takeout endpoints) headers. Read more about it in [`TVM`](#tvm).

## Debug tools

At some point, you'll need to decode or encode the `public_id` of the shared list(s).
To do this easily - use the special `NPM` scripts:

```sh
<- npm run encode 1 2 # 1 - id, 2 - seed
-> 2021-07-21T08:49:08.657Z - info: gKZ-xkEC

<- npm run decode gKZ-xkEC
-> 2021-07-21T08:49:35.305Z - info: {id: 1, seed: 2}

<- npm run encode -- 1 -2 # '--' is necessary with the negative arguments; 1 - id, -2 - seed
-> 2021-07-21T08:49:08.657Z - info: f6Z-xkH-

<- npm run decode f6Z-xkH-
-> 2021-07-21T08:49:35.305Z - info: {id: 1, seed: -2}
```

These scripts require the source code to be compiled. Make sure you've executed `make build`
before start using them (check: `./out/app/tools/public-id.js` exists)

## Database

### Connect to the database
To connect to the local database server with psql simply run:
```sh
make db-connect
```

For connecting to other environments use the `DB_ENV` variable

For production
```sh
make db-connect DB_ENV=testing
```

### Running tests for migrations changes

If you're changing a migration file (`/db/migrations/*`) you will need a clean version of the DB, so that your changed
migration is applied. You can do this by stopping the container with the local DBMS before running the tests:
```
make db-local-stop test
```

### Cloud environments

We have a [MDB cluster](https://yc.yandex-team.ru/folders/foonquium8istgt59qca/managed-postgresql?section=list) for the databases in the cloud environments

## Testing

For run all tests and validation procedures use the command:

```sh
make validate
```

### Tests structure

* All tests are placed in [src/tests](src/tests) directory.
* Files with tests have `.test.ts` extension. Files with `.ts` extension contains test utilities.
* Tests are separated by types.

### Unit tests

```sh
make run-test-unit
```

* Unit tests **must** check only the functionality of one module and **must not** make real HTTP requests or communicate with a database.
* Unit tests **must** repeat file structure from source directory, e.g. `src/tests/unit/lib/string-helper.test.ts` is a test for `src/app/lib/string-helper.ts` module.
* Don't try to write unit test for everything. Sometimes it's easier and better to write integration or functional test.

### Integration tests

```sh
make run-test-integration
```

* Integration tests check integration of application with database or with some another HTTP API.
* Unlike unit tests, integration tests *must not* repeat the file structure from source directory. Instead, they should be grouped by meaning.
* Don't rely to order of records in query result from database. See https://www.postgresql.org/docs/current/static/queries-order.html

### TVM

For the local development and testing [TVM-daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/) in `unittest` mode is used. Dev-time tickets must be generated using the [tvmknife](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife)
tool:

```sh
# All commands below will send the tickets to the stdout
ya tool tvmknife unittest user -e prod -d <STUB UID> # Generate user ticket
ya tool tvmknife unittest service -s 2 -d 1 # Generate maps service ticket
ya tool tvmknife unittest service -s 3 -d 1 # Generate mobmaps-proxy-api service ticket
ya tool tvmknife unittest service -s 4 -d 1 # Generate takeout service ticket
```

### Stress tests

About stress testing see [src/tests/stress/README.md](src/tests/stress/README.md).

## Blackbox

In testing and dev environments we use blackbox-mimino. Grants:
* Prod
    * https://st.yandex-team.ru/PASSPORTGRANTS-6947
* Mimino
    * https://st.yandex-team.ru/PASSPORTGRANTS-6652
    * https://st.yandex-team.ru/PASSPORTGRANTS-6653
* Stress
    * https://st.yandex-team.ru/PASSPORTGRANTS-6986

We have [test user](https://yav.yandex-team.ru/secret/sec-01f127w43gq06wz4r2fxe0xf7m/explore/version/head) to go to blackbox (get a `public_name`)
and check the functionality of the service.

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
make db-migrate
```

By default the migration is applied to the `development` environment. If you wish to target the testing environment for example,
set the `DB_ENV` variable to `testing`
```sh
make db-migrate DB_ENV=testing
```

Another defaultly set parameter is the dry-run flag. If you are sure you want to apply the migration pass `DB_MIGRATE_DRY_RUN=0`:

```sh
make db-migrate DB_MIGRATE_DRY_RUN=0
```

If needed a specific target revision of the migrations can applied using the `DB_MIGRATE_TARGET` variable:
```sh
make db-migrate DB_MIGRATE_TARGET=3
```
The default version is `latest`.

Let's say you want to apply version `3` of the schema to the `testing` cluster. You should type in:

```sh
make db-migrate DB_ENV=testing DB_MIGRATE_TARGET=3
# make sure there were no errors in the output
make db-migrate DB_ENV=testing DB_MIGRATE_TARGET=3 DB_MIGRATE_DRY_RUN=0
```

## GDPR

### Takeout: `/v1/takeout`, `/v1/takeout/lists/...`

By GDPR user can request all his personal data from service. We use [synchronous](https://wiki.yandex-team.ru/passport/takeout/integration/#sinxronnyjjmexanizmvygruzkidannyx) integration.

To test integration:
```
# TODO
```

### Takeout Delete: `/v1/takeout/delete`, `/v1/takeout/status`

By GDPR user can manually delete his personal data from service. We use synchronous integration and remove user's data right inside delete request without any extra scheduling.

* [High level architecture and goals](https://wiki.yandex-team.ru/users/4ernyakov/takeout-2.0/)
* [Integration API requirements](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/)

To test integration:
```
# TODO
```

### Processing deleted accounts

// TODO - To be done

## Duty Guides

See the full list of the duty guides in an [appropriate document](./docs/duty.md)

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [SQL](docs/internal/sql-style-guide.md)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Troubleshooting

### macOS and make errors
If you're using macOS and when running any make target you encounter errors sucha as:
```
Makefile:4: *** missing separator.  Stop.
```
you should get a fresh version of make through `brew install make`.
The error is caused by the `undefine` keyword which is not available in the macOS default version of make.

### db-connect, macOS and MDB
If you're running `make db-connect` or `make db-migrate` on macOS and trying to target remote MDB clusters
you will encouter connection errors. This is because by default these targets are ran in docker containers
and docker on macOS cannot connect to IPV6-only hosts, such as the hosts of our PG clusters.

As a workaround, if you have `psql` and/or `pgmigrate` installed you can use them instead of the docker-packed
executables:
```sh
export PSQL_EXECUTABLE=psql
make db-connect DB_ENV=production # this will use the host machine psql instead of the docker-contained

export PGMIGRATE_EXECUTABLE=pgmigrate
make db-migrate DB_ENV=prodcution # the same is valid for pgmigrate
```

### connect to docker

If you have problems with connecting to the database in docker, you can try:
- if you have an instance of PostgreSQL installed locally - try to stop it (e.g. `brew services stop postgresql`) and relaunch your OS first;
- remove unnecessary entries from `/etc/hosts`;
- restart the laptop.
