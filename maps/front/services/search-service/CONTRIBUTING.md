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
   npm ci
   make dev.setup
   ```

3. Build and run the service in development mode:

   ```sh
   make
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

## Manual testing
Check that search are working in jsapi:

| Api version | URL |
|--|--|
| 1.1 | https://api-maps.tst.c.maps.yandex.ru/1.1/tests/html/mapcontrolsadding.html |
| 2.0 | https://api-maps.tst.c.maps.yandex.ru/2.0/tests/controls/search.html |
| 2.1 | https://api-maps.tst.c.maps.yandex.ru/2.1/tests/manual/cases/control/search/basic.html |

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the cloud platform Deploy.

### Release to testing

Just merge your PR into trunk and it will be automatically deployed to testing.

### Deploy the current version to production

```sh
npx qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
