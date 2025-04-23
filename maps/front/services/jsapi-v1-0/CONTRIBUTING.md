# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

2. Install dependencies:

   ```sh
   make deps
   ```

3. Build and run the service in development mode:

   ```sh
   make dev
   ```

By default http-service starts listening on port `8080`. If you started the application locally it
should respond on http://localhost:8080/ping

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment
variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all tests use the command:

```sh
make validate
```

For smoke tests:

1. Deploy project to testing
2. Open tests/index.html

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

### Release to testing

```sh
make patch # or minor, major
npx qtools release testing
```

### Deploy the current version to production

```sh
npx qtools deploy production
```

## Stress test
```sh
npx qtools deploy stress
make test-stress
```

Clean afterwards with:
```sh
make test-stress-clean
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
