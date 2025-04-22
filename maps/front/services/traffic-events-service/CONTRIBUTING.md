# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n).

## Getting Started

1. Install dependencies:

  ```
  npm ci
  ```

3. Build and run the service in development mode:

  ```
  make dev
  ```

By default http-service starts listening on port `8080`. If you started the application locally it should respond on:
```
http://localhost:8080/v1/stub_endpoint
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all tests use the command:

```
make validate
```

## Manual testing
Check that traffic are working in jsapi:

| Api version | URL |
|--|--|
| 1.1 | https://api-maps.tst.c.maps.yandex.ru/1.1/tests/html/traffic-with-infolayer.html |
| 2.0 | https://api-maps.tst.c.maps.yandex.ru/2.0/tests/controls/traffic.html |
| 2.1 | https://api-maps.tst.c.maps.yandex.ru/2.1/tests/manual/cases/control/traffic/basic.html |


## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

To deploy a new version of the application just update version and push changes to remote server:

```sh
make patch # or minor, major
```

### Build and push image

```
./node_modules/.bin/qtools build
./node_modules/.bin/qtools push
```

### Deploy the current version

```
./node_modules/.bin/qtools deploy testing
or
./node_modules/.bin/qtools deploy production
```

## Project Structure

```
configs         Configuration files for different environments
docs            Project's public API documentation
src/            Project's source code
  middlewares   Main middlewares which process request
  lib           Utilities and project-level libraries
  utils         Helpers for coding
tests           Tests
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
