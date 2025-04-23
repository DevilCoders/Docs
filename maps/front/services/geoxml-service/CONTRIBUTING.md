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

2. Install dependencies and setup hosts for local development:

   ```sh
   make deps hosts
   ```

3. Build and run the service in development mode:

   ```sh
   make dev
   ```

By default http-service starts listening on port `8080`. If you started the application locally it
should respond on http://localhost:8080/ping

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all validations use the command:

```sh
make validate
```

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the cloud platform Deploy.

### Release to testing

```sh
make patch # or minor, major
arc pr create --push --publish --auto
# after merging to trunk
./node_modules/.bin/qtools release testing
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

### Stress testing
```sh
make test-stress
```

After shooting remove stage:
```sh
make test-stress-clean
```

## Project Structure

```
@types          Typescript types declarations
docs            Project's public API documentation
src             Project's source code
  app           API handlers and libraries
    middleware  Using middlewares
    lib         Utilities and project-level libraries
    parsers     Geoxml parsers for transform (KML, GMX, YMAPS) to JSON format
    utils       Helpful utils functions
  tests         Tests
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
