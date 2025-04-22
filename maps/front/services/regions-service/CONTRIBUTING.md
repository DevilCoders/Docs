# Contributing

The maintainer accepts pull requests and has the right to reject them if they doesn't meet project's standards.
If you have a bug report or a feature request, please use the project's
[task queue](https://github.yandex-team.ru/mapsapi/regions-service#general-information).
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.
Before writing any code, please take a look at the [codestyle](https://github.com/ymaps/codestyle) used in the codebase.
Before sending your pull request, please check that the list tools and the unit tests pass.

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](https://github.yandex-team.ru/mapsapi/http-api-stub/blob/master/Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [nvm](https://github.com/nvm-sh/nvm).

## Getting Started

1. Clone repository

2. Install dependencies:

  ```
  npm ci
  ```

3. Run the service in development mode:

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

## Deploying a Release to Testing

This project uses [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools) (qtools for short) to interface with docker, the docker registry and the cloud platform qloud.

Assuming you have qtools up and running now you can release a new patch version of the application to testing by just running:
```
make patch
make release-testing
```

## Updating data

1. Process data with [regions-tools](https://github.yandex-team.ru/mapsapi/regions-tools)
2. Make sure to make a backup of curently available data to restore it in case of emergency
3. Upload data to S3-MDS (see 'S3 MDS access' and 'Bucket structure' sections for details)

#### S3 MDS access

See [https://wiki.yandex-team.ru/mds/s3-api/](https://wiki.yandex-team.ru/mds/s3-api/)

#### Bucket structure

```
s3://regions-service/test_data/1.0 test data for regions v1
s3://regions-service/test_data/v2 test data for regions v2

s3://regions-service/data/1.0 production data for regions v1
s3://regions-service/data/v2 production data for regions v2
```

## Project Structure

```
configs         Configuration files for different environments
docs            Project's public API documentation
src/            Project's source code
  middlewares   Middlewares
  lib           Utilities and project-level libraries
tests           Tests
```
