# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

```sh
nvm use
npm ci
make dev.setup
make dev                        # http://localhost:8080/ping

MAPS_NODEJS_PORT=9999 make dev  # http://localhost:9999/ping
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

```sh
make patch # or minor, major
arc pr create --push --no-edit --publish
./node_modules/.bin/qtools release testing
```

CI will do the rest.

Or if you want to do it bare handed:
```sh
./node_modules/.bin/qtools release testing
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
