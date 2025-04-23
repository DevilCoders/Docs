# Contribution Guide

The maintainer accepts pull requests and has the right to reject them if they doesn't meet project's standards.
If you have a bug report or a feature request, please use the project's
[task queue](https://github.yandex-team.ru/maps/discovery-int#general-information).
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.

## Codestyle

Before writing any code, please take a look at the:

- [Yandex Maps codestyle](https://github.com/ymaps/codestyle)
- [HTTP API conventions](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Pull-requests

If you fixed or added something useful to the project, you can send pull-request.
It will be reviewed by maintainer and accepted, or commented for rework, or declined.
Before sending your pull request, please check that the lint tools and the unit tests pass.

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](https://github.yandex-team.ru/maps/http-api-stub/blob/master/Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n) or [nvm](https://github.com/creationix/nvm).

## Getting Started

### 1. Install dependencies

```sh
cd maps/front/services/discovery-admin && \
nvm use && \
make deps
```

### 2. Run discovery-int

Follow instructions from `/arcadia/maps/front/services/discovery-int/CONTRIBUTING.md`

### 3. Run discovery-admin in development mode

```sh
make dev
```

By default http-service starts listening on port `8080`. If you started the application locally it should respond on:

```
https://username.maps.dev.yandex.ru:8080/ping // username - yandex-team login
https://localhost:8080/ping
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```sh
MAPS_NODEJS_PORT=8666 make dev
```

## Testing

For code sanity check (codestyle) run:

```sh
make validate
```

For run tests run:

```sh
make tests
```

## Deploying

This project uses [ymaps-qloud-tools](https://github.yandex-team.ru/maps/ymaps-qloud-tools)
(`qtools` for short) to interface with docker, the docker registry and the cloud platform Qloud.

To deploy a new version of the application update version.

```sh
make patch # minor
```

The pull request merge will trigger a **CI (Arc)** build which:

1. Run tests.
2. Builds a docker image.
3. Pushes it to registry.
4. Deploys it to testing.

This is the preferred way to deploy.

### Manual release to testing

If CI is down, use the following steps:

```
make release-testing
```

### Deploy the current version to production

```
make deploy-production
```
