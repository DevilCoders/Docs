# Contribution Guide

## Codestyle

Before writing any code, please take a look at the:

- [Yandex Maps codestyle](https://github.com/ymaps/codestyle)
- [HTTP API conventions](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](https://github.yandex-team.ru/maps/http-api-stub/blob/master/Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n) or [nvm](https://github.com/creationix/nvm).

## Getting Started

### 1. Install dependencies

```sh
cd maps/front/services/discovery-int && \
nvm use && \
make deps
```

### 2. Install docker image with postgresql

Next command create empty test and development databases in docker.

```sh
make db-start
make db-migrate ENVIRONMENT=development MIGRATE_VERSION=latest
```

For reloading database

```sh
docker rm ${image_name}
make db-start
```

### 3. Setup database for development

Create `.env` file containing following variables:

```
POSTGRES_DATABASE=discovery_int
POSTGRES_PASSWORD=password
POSTGRES_USERNAME=discovery_user
```

Use `.env.example` for example.

### 4. Start migration

Migrate schema:

```sh
make migrate-db ENVIRONMENT=development MIGRATE_VERSION=latest
make migrate-db ENVIRONMENT=integration-tests MIGRATE_VERSION=latest
```

Also you can get data from real database:

```sh
pg_dump -Fc 'postgresql://${user}:${password}@${host}:${port}/${database_name}' > /tmp/discovery_int.dump
pg_restore -d 'postgresql://discovery_user:password@localhost:6432/discovery_int' /tmp/discovery_int.dump
```

### 5. Run the service in development mode

```sh
make dev
```

By default http-service starts listening on port `8081`. If you started the application locally it should respond on:

```
http://localhost:8081/ping
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For code sanity check (codestyle) run:

```sh
make validate
```

For run tests run:

```sh
make tests
```

## Deploying

This project uses [qloud tools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools)
(`qtools` for short) to interface with docker, the docker registry and the cloud platform Qloud.

> Don't forget to install [ya](https://wiki.yandex-team.ru/yatool/).

To deploy a new version of the application update version.

```sh
make patch # minor
```

The pull request merge will trigger a **CI (Arc)** build which:

1. Run tests.
2. Builds a docker image.
3. Pushes it to registry.
4. Deploys it to testing.

This is the preferred way to deploy.

**DON'T FORGET TO MIGRATE DATABASE CHANGES, IF IT'S EXIST**

1. Change file `.env` for necessary environment data
2. Run command: `ENVIRONMENT=<env> MIGRATE_VERSION=<version | latest> make migrate-db`

### Manual release to testing

If CI is down, use the following steps:

```
make release-testing
```

### Deploy the current version to production

```
make deploy-production
```
