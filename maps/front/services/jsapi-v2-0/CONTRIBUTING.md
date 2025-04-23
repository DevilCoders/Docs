# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

```sh
nvm use
make deps
make dev.setup
make dev

MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For run all tests use the command:

```sh
make validate
```

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the [Y.Deploy](https://deploy.yandex-team.ru/) cloud platform.

```sh
npx qtools release testing

npx qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
