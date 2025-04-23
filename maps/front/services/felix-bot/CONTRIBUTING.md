# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.

* [Node.js](http://nodejs.org/) `10`

The project use [nvm](https://github.com/creationix/nvm) to choose the preferred nodejs version. Just run in the root of the project:

```sh
nvm use
```

Also you should install [`tvmknife`](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife).

## Getting Started

> Before starting copy `.secrets.example.json` to `.secrets.json` and specify tokens for bots.
> You can use next secret: https://yav.yandex-team.ru/secret/sec-01epy5kw0s9bazxftd30dxngx4/explore/versions

```sh
make
```

By default http-service starts listening on port `8080`. If you started the application locally it should respond on:
```
http://localhost:8080/ping
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```
MAPS_NODEJS_PORT=8666 make dev
```

## Debugging

In VS Code you can debug process via `Inspect server` configuration. Firstly, start server:

```sh
make dev
```

Then start debugger `Inspect server` and choose process with `node --nolazy -r ts-node/register ./src/app.ts`.

> After restart server you should choose process again.

## Testing

For run all tests use the command:

```sh
make test
```

For run all linters and spec validator use command:

```sh
make validate
```

## Deploying

This project uses [`qtools`](github.yandex-team.ru/maps/infra/tree/master/packages/qtools) to interface with docker, the
docker registry and the cloud platform Deploy.

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

### Manual release to testing

If CI is down, use the following steps:

```
./node_modules/.bin/qtools release testing
```

### Deploy the current version to production

```
./node_modules/.bin/qtools deploy production
```

## Project Structure

```
docs            Project's public API documentation
src/            Project's source code
  app/
    config        Configuration files for different environments
    lib           Utilities and project-level libraries
    middlewares   Express-middlewares for requests
    v1            API handlers and libraries for version 1
  tests/          Tests
tools           Tools for CI and other
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
