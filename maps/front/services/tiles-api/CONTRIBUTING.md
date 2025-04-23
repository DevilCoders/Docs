# Contributing

The maintainer accepts pull requests and has the right to reject them if they does not meet project's standards.
If you have a bug report or a feature request, please use the project's
[task queue](https://a.yandex-team.ru/arc_vcs/maps/front/services/tiles-api#general-information).
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.
Before writing any code, please take a look at the [codestyle](https://github.com/ymaps/codestyle) used in the codebase.
Before sending your pull request, please check that the list tools and the unit tests pass.

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

```sh
# 1. Switch to correct Node.js version
nvm use
# 2. Install dependencies and setup hosts for local development
make deps hosts secrets
# 3. Start service in the development mode on port 8080
make dev
MAPS_NODEJS_PORT=8666 make dev # Optionally override port
```

## Testing

```sh
make validate # single command to check everyhting below

make lint
make validate-api-doc
make test

make test MOCHA_EXTRA_OPTIONS='-g foo' # run specific tests
```

### Stress tests

```sh
make test-stress           # Run stress tests
make test-stress-clean     # Don't forget to undeploy stress environment
```

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools) to interface with docker, the
docker registry and the cloud platform Yandex Deploy.

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

## Project Structure

```
configs         Configuration files for different environments
docs            Project's public API documentation
src/            Project's source code
  lib           Utilities and project-level libraries
  middlewares   Express middlewares
  v1            API handlers and libraries for version 1
tests           Tests
```
