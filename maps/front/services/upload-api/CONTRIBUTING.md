# Contributing

The maintainer accepts pull requests and has the right to reject them if they doesn't meet project's standards.
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.
Before writing any code, please take a look at the [codestyle](https://github.com/ymaps/codestyle) used in the codebase.
Before sending your pull request, please check that the list tools and the unit tests pass.

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](https://github.yandex-team.ru/mapsapi/http-api-stub/blob/master/Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n).

Also don't forget about [ya](https://wiki.yandex-team.ru/yatool/).

## Getting Started

1. Clone repository
2. Install dependencies:

  ```
  make install
  ```

3. Create local https certificate:

  ```
  make create-cert
  ```

  Add this certificate as trusted to your system toolchain. This is needed for requests to blackbox.

4. Add `$(whoami).maps.dev.yandex.*` domains as aliases to localhost to your system `/etc/hosts`:

  ```
  make patch-etc-hosts
  ```

5. Run the service in development mode:

  ```
  make dev-https
  ```

By default https-service starts listening on port `8080`. If you started the application locally it should respond on:
```
https://$(whoami).maps.dev.yandex.ru:8080/v1/stub-endpoint
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```
MAPS_NODEJS_PORT=8666 make dev-https
```

## Testing

For run all tests use the command:

```
make validate
```

## Deploying a Release to Testing

This project uses [ymaps-qloud-tools](https://github.yandex-team.ru/maps/ymaps-qloud-tools) (qtools for short) to interface with docker, the docker registry and the cloud platform qloud.
For qtools to work properly please check out the project's [docs](https://github.yandex-team.ru/maps/ymaps-qloud-tools#configuration) on how to configure it.
Note that the application name in the cloud platform should be prefixed with `front-`, if you will be deploying to the [maps project](https://platform.yandex-team.ru/projects/maps).

Assuming you have qtools up and running now you can release a new patch version of the application to testing by just running:
```
make patch
make release-testing
arc pr create --push --publish
```

## Deploying to production

```
make release-production
```

Then merge your PR.

## Makefile Targets

There are common `Makefile` targets:

| Target name | Description |
|---|---|
| `make install` | Install dependencies (e.g. `npm` dependencies) |
| `make dev` | Run application in development mode |
| `make dev-https` | Run application in development mode with https server |
| `make validate` | Run all checks and tests |
| `make validate-api-doc` | Check swagger specification of API documentation by schema |
| `make lint` | Check js files using [eslint](http://eslint.org/) |
| `make test` | Run tests (unit, integration, functional) |
| `make prepublish` | Prepare the files of the project for packaging |
| `make patch` | Bumps the patch version of the project in `package.json` |
| `make minor` | Analogous to `patch`, with the difference that it bumps the minor version |
| `make release-testing` | Builds and uploads an image with the latest version. Then creates an deploy draft in the cloud platform |

## Project Structure

```
configs         Configuration files for different environments
docs            Project's public API documentation
src/            Project's source code
  v1            API handlers and libraries for version 1
  lib           Utilities and project-level libraries
tests           Tests
```
