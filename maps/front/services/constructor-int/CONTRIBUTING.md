# Contributing

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Contributing](#contributing)
  - [Table of Contents](#table-of-contents)
  - [Requirements](#requirements)
  - [Getting started](#getting-started)
  - [Testing](#testing)
    - [Tests structure](#tests-structure)
    - [Unit tests](#unit-tests)
    - [Integration tests](#integration-tests)
    - [Debugging in tests](#debugging-in-tests)
    - [TVM](#tvm)
    - [Stress tests](#stress-tests)
      - [Run tests](#run-tests)
      - [Update ammo](#update-ammo)
  - [Deploying](#deploying)
    - [Release to testing](#release-to-testing)
    - [Deploy the current version to production](#deploy-the-current-version-to-production)
  - [Deployment validation](#deployment-validation)
  - [Schedulers](#schedulers)
  - [Database](#database)
    - [Migrations](#migrations)
      - [Creating](#creating)
      - [Applying](#applying)
  - [GDPR](#gdpr)
    - [Takeout: `/v2/takeout`, `/v2/takeout/maps/...`](#takeout-v2takeout-v2takeoutmaps)
    - [Takeout Delete: `/v2/takeout/delete`, `/v2/takeout/status`](#takeout-delete-v2takeoutdelete-v2takeoutstatus)
    - [Processing deleted accounts](#processing-deleted-accounts)
  - [Style guides](#style-guides)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Requirements

* [nvm](https://github.com/creationix/nvm)
* docker
* docker-compose
* python 3 and pip (for database migrations and maintenance)
* xmllint (for testing)

## Getting started

```sh
nvm use
pip install --user pipenv

npm ci
pipenv install --dev

make db-local-start
make migrate-db

make                            # http://localhost:8080/ping
MAPS_NODEJS_PORT=9999 make dev  # http://localhost:9999/ping
```

## Testing

For run all tests use the command:

```sh
make validate
```

### Tests structure

* All tests are placed in [tests](tests) directory.
* Files with tests have `.test.ts` extension. Files with `.ts` extension contains test utilities.
* Tests are separated by types.

### Unit tests

* Unit tests *must* check only the functionality of one module and *must not* make real HTTP
  requests or communicate with a database.
* Unit tests *must* repeat file structure from source directory, e.g. `tests/unit/lib/di.test.ts`
  is a test for `src/lib/di.ts` module.
* Don't try to write unit test for everything. Sometimes it's easier and better to write integration
  or functional test.

### Integration tests

* Integration tests check integration of application with database or with some another HTTP API.
* Unlike unit tests, integration tests *must not* repeat the file structure from source directory.
  Instead, they should be grouped by meaning.
* Don't rely to order of records in query result from database. See https://www.postgresql.org/docs/current/static/queries-order.html

### Debugging in tests

If you need debug some tests, use the following steps:

1. Add `debugger` statement in code.
2. Run `mocha` with `--inspect-brk` argument:

   ```sh
   make test MOCHA_EXTRA_OPTIONS='--inspect-brk'
   # Or if build-watch target is running
   make run-test MOCHA_EXTRA_OPTIONS='--inspect-brk'
   ```

3. Connect to Node.js process using [inspector protocol](https://nodejs.org/en/docs/inspector/).

### TVM

For testing [TVM-daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/) in `unittest` mode
is used. Tickets are generated with [tvmknife](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife)
tool.

### Stress tests

#### Run tests

To run all stress tests call:

```sh
node out/tests/stress/run-tests.js -t capacity
```

To test specific endpoints call:

```sh
node out/tests/stress/run-tests.js -e 'GET /v2/maps' -t capacity
```

`stress` environment will be deployed automatically. Don't forget undeploy it when you finish:

```sh
./node_modules/.bin/qtools undeploy --force stress
```

#### Update ammo

1. Generate ammo.

  Preparing:

  * Install [tvmknife](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife).
  * Install [yav](https://vault-api.passport.yandex.net/docs/#cli) utility (optional).

  Then call:

  ```sh
  # Get secrets with `yav` utility, or use web interface instead.
  secret_version=$(yav list secrets -q constructor-int_testing -j | jq -r '.[].last_secret_version.version')

  # Change in development.json
  dbUser: value of $(yav get version $secret_version -o dbUser)
  dbPassword: value of $(yav get version $secret_version -o dbPassword)

  # Generate ammo.
  MAPS_STAGE=make-ammo node out/tests/stress/gen-ammo.js \
     --tvmknife $(ya tool tvmknife --print-path)
  ```

  where `sas-5of6uqbf4wrtkx0q.db.yandex.net` is database host for `stress` environment.

  *Note:* standard PostgreSQL [environment variables](https://www.postgresql.org/docs/11/libpq-envars.html)
  can be used with/without connection string.

  You can generate ammo for specific endpoints using `-e` option:

  ```sh
  node out/tests/stress/gen-ammo.js -e 'GET /v2/maps' ...
  ```

2. Upload ammo. Ammo are stored in [MDS S3](https://wiki.yandex-team.ru/mds/s3-api/).

   Preparing:

   * Request `admin` role to the current service in IDM: https://wiki.yandex-team.ru/mds/s3-api/authorization/#vydachapravrobotuilisotrudniku
   * Install and setup AWS CLI tool: https://wiki.yandex-team.ru/mds/s3-api/s3-clients/

   Then copy files to MDS S3:

    ```sh
    aws s3 --endpoint-url=http://s3.mds.yandex.net cp ammo s3://constructor-int-ammo --recursive
    ```

    where `ammo` is directory with generated ammo.

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

### Release to testing

```sh
make patch # or minor, major
npx qtools release testing --force
```

### Deploy the current version to production

```sh
npx qtools release production --force
```

## Deployment validation

Once the deployment process of an appropriate environment is done - you can visit the `Constructor` UI that is using `constructor-int` endpoints under the hood in order to check if everything is fine.

| Environemt | Constructor UI URL |
|---|---|
| Testing | https://l7test.yandex.ru/map-constructor/ |
| Production | https://yandex.ru/map-constructor/ |

Make some changes (e.g. create the map, create new objects, edit its descriptions or visual properties) and save it. After that, you should be able to view the logs produced by the service in response to your request. In order to achieve that - go to the [`maps-front-constructor` project in Y.Deploy](https://yd.yandex-team.ru/projects/maps-front-constructor), select the needed environment, ssh to one of the hosts (unfortunately, we can't predict what the host exactly had processed your request. So the only acceptable option here - is to ssh on all the hosts) and look at the `access-tskv.log` file:

```sh
ssh <host>
less +G /var/log/nginx/access-tskv.log # +G option will show the file starting from the end - so the most recent requests will be shown
```

Make sure that your request has been processed on one of the hosts and didn't produce the errors.

## Schedulers

[Schedulers](schedulers) are managed by [lama](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/lama) and [bean](https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean) with [binary scheduler](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/lama/presets/projects/maps-front/binary-scheduler.jinja) preset.

## Database

### Migrations

For database migrations [sqlalchemy-migrate](https://github.com/openstack/sqlalchemy-migrate) tool
is used. Project migrations are stored in [migrations](migrations) directory.

#### Creating

For creating migration call:

```sh
pipenv run migrate script_sql postgresql "some_clear_description" migrations/constructor
```

This command creates two files in [migrations/constructor/versions](migrations/constructor/versions)
directory (for upgrade and downgrade). Keep downgrade file empty if downgrading doesn't make sense.

#### Applying

1. Detect `master` host of the needed [MDB cluster configuration](README.md#storage)
   from web interface, or using `yc` command line tool:

   ```sh
   yc postgres cluster list --folder-name maps-front-constructor-int
   yc postgres hosts list --cluster-name <cluster-name> --folder-name maps-front-constructor-int --format json | jq '.[] | select(.role == "MASTER") | .name'
   ```

2. Apply migrations:

   ```sh
   pipenv run tools/migrate_db.py postgresql://<user>:<password>@<dbhost>:6432/constructor migrations/constructor
   ```

   where:

   * `dbhost` is master database host.
   * `user` and `password` are values from [vault](README.md#vault).
   * `migrations/constructor` is path to local directory [migrations/constructor](migrations/constructor).

## GDPR

### Takeout: `/v2/takeout`, `/v2/takeout/maps/...`

By GDPR user can request all his personal data from service.
We use [synchronous](https://wiki.yandex-team.ru/passport/takeout/integration/#sinxronnyjjmexanizmvygruzkidannyx) integration.

To test [integration](https://wiki.yandex-team.ru/passport/takeout/integration/#testirovanieintegracii):

```sh
# Issue service ticket from constructor-int testing to takeout testing.
# Find your <secret> value here: https://abc.yandex-team.ru/services/maps-front-constructor-int/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granting&state=granted&view=consuming>
# Select the needed environment and grab the value of `client_secret` property
$ tvmknife get_service_ticket client_credentials -s 2010780 -d 2009783 -S <secret>
# Connect to host from https://yd.yandex-team.ru/stage/maps-front-constructor-int_testing/
$ ssh <address>
# Run integration tests with the specified uid and ticket.
$ curl -X POST "https://takeout-test.passport.yandex.net/1/debug/run_integration_test/?consumer=maps-front-constructor-int" -d "uid=$uid&service_name=maps_constructor" -H "X-Ya-Service-Ticket: $ticket"
# Check task status. $extract_id must be present in the successful result of the previous request
$ curl -X POST "https://takeout-test.passport.yandex.net/1/debug/get_status/?consumer=maps-front-constructor-int" -d "uid=$uid&extract_id=$extract_id&service_name=maps_constructor" -H "X-Ya-Service-Ticket: $ticket"
```

After creating task, you can check requests from `Takeout` in logs of as described in [Deployment validation](#deployment-validation) chapter:

```sh
ssh <host>
less +G /var/log/nginx/access-tskv.log
```

Having the `uid` and `extract_id` you can ask the [Passport project duty](https://abc.yandex-team.ru/services/passp) to validate that GDPR-upload has the correct format. They could help to validate only testing data that do not belong to any external customers (i.e. you should request the GDPR-upload using only your own `uid`)

If you're trying to validate the GDPR-upload in production - you don't need to request assistance from anyone. Just visit the [pproduction passport page](https://passport.yandex.ru/profile/getdata), log in with your external Yandex account, and request the data uploading using the UI. Once your data upload will be done (it may take hours to prepare the full archive) - you'll receive the archive with your data and could validate it manually.

### Takeout Delete: `/v2/takeout/delete`, `/v2/takeout/status`
By GDPR user can manually delete his personal data from service.
We use synchronous integration and remove user's data right inside delete request without any extra scheduling.
- [High level architecture and goals](https://wiki.yandex-team.ru/users/4ernyakov/takeout-2.0/)
- [Integration API requirements](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/)
- More in [MAPSCONSTRUCTOR-1906](https://st.yandex-team.ru/MAPSCONSTRUCTOR-1906)

To test integration:
```sh
# TODO
```

### Processing deleted accounts

[Deleted accounts](https://wiki.yandex-team.ru/passport/deleted_accounts/) are processed asynchronously using [sync-deleted-uids](schedulers/sync-deleted-uids) binary scheduler.

Notes:

* All communications with `YT` are performed from
  [robot-maps-ctor](https://staff.yandex-team.ru/robot-maps-ctor) robot.
* Temporary `YT` and `YQL` data are stored in `//home/maps/front/constructor-int/tmp` directory for
  security reasons.
* Therefore, `robot-maps-ctor` needs access in [IDM](https://idm.yandex-team.ru) to the following groups:
    * `YT-Hanh -> passport-data-ro`
    * `YT-Hahn -> constructor-int`
* Deleted maps are logged to `deleted_maps_log` table in `PostgreSQL`.

To test integration locally, run:

```sh
YT_TOKEN=<valid YT and YQL token> make run-test-schedulers
```

Note, that as `YT_TOKEN` you should actually provide a [YQL token](https://yql.yandex-team.ru/oauth), which gives access for both YT and YQL APIs.

Also note, that these tests are slow (~5 minutes).

## Style guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [SQL](docs/internal/sql-style-guide.md)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
