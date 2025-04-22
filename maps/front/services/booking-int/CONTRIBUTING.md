# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

2. Install dependencies:

   ```sh
   npm install
   ```

3. Install secrets:

   ```sh
   make install-secrets
   ```

4. Launch db and app:

   ```sh
   make db-start
   make db-add-data
   make dev # <- separate terminal
   ```

By default http-service starts listening on port `8080`. If you started the application locally it
should respond on https://booking-int.dev.yandex-team.ru:8080/ping

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all tests use the command:

```sh
make validate
```

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools) to interface with docker, the
docker registry and the cloud platform Yandex Deploy.

### Release to testing

Testing is released automatically when your review request is merged to trunk

### Deploy the current version to production

```sh
make deploy-production
```

### Migrating database

We use [pgmigrate](https://github.com/yandex/pgmigrate) to migrate PostgreSQL DB.

#### Installation (MacOS):

Steps may vary depending on your current configuration. These are all the prerequisites.

`brew install postgresql`
`brew install python3`
`pip3 install yandex-pgmigrate`

```sh
make db-migrate-(production|testing)
```

Make sure you have access to all corresponding secrets. They will be used for database connection.

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Utilities

We use VSCode, all the necessary extensions are added as suggested extensions to current workspace.
