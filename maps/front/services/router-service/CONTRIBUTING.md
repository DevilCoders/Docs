# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Clone repository

   ```sh
   cd ~/arcadia/maps/front/services/router-service
   ```

2. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

3. Install dependencies:

   ```sh
   make deps
   ```

4. Build and run the service in development mode:

   ```sh
   make
   ```

By default http-service starts listening on port `8080`. If you started the application locally it
should respond on http://localhost:8080/ping

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all tests use the command:

```sh
make validate
```
## Manual testing
Check that routes are working in 2.1.
- https://api-maps.tst.c.maps.yandex.net/2.1.77/tests/manual/cases/route/basic.html
- https://api-maps.tst.c.maps.yandex.net/2.1.77/tests/manual/cases/multiRouter/basic.html

### Stress tests

To run stress tests call:

```sh
make test-stress
```

`stress` environment will be deployed automatically. Don't forget undeploy it when you finish:

```sh
make test-stress-clean
```

For more information about stress testing see [src/tests/stress/README.md](src/tests/stress/README.md).

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arcadia/maps/front/packages/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

> Need qtools [authorization token](https://a.yandex-team.ru/arcadia/maps/front/packages/qtools#authorization)

### Release to testing

```sh
make patch # or minor, major
./node_modules/.bin/qtools release testing
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

## How to check service in testing

Get a JS API token.
```
JSAPI_TOKEN=`curl -s "https://api-maps.yandex.ru/2.0/?lang=ru_RU" | grep token | awk -F "\"" '{print $16}'`
```

Send a request. For example,
```
curl -s "https://api-maps.tst.c.maps.yandex.ru/services/route/v2/masstransit/stop?uri=ymapsbm1%3A%2F%2Ftransit%2Fstop%3Fid%3Dstation__9858796&lang=ru_RU&token=$JSAPI_TOKEN"
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
