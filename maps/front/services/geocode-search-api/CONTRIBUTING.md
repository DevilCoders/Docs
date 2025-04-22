# Contributing

## Requirements
The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n).

Extra dependencies which are need for testing issues:
  * [xmllint](http://xmlsoft.org/xmllint.html)
  * [diff](https://linux.die.net/man/1/diff)

## Getting Started

1. Install dependencies:

  ```
  make deps dev.setup
  ```

3. Build project and run the service in development mode:

  ```
  make
  ```

By default http-service starts listening on port `8080`. If you started the application locally it should respond on:
```
http://localhost:8080/search/v1/
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```
MAPS_NODEJS_PORT=8666 make
```

## Testing

For run all tests use the command:

```
make validate
```

### Update mocks for functional tests
```
NOCK_SAVE=1 make test-functional
```

### Acceptance tests
```
make test-acceptance
```

## Stress tests
For run all stress tests use the command:

```
make test-stress
```

### [Update ammo](src/tests/stress)

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
  app/          App's source code
  tests         Tests
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
