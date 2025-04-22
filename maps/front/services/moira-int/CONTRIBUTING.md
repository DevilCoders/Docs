# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Install `docker-compose`
Example:

    ```sh
    pip install docker-compose
    ```

2. Install `ya`. See https://wiki.yandex-team.ru/yatool/distrib/

3. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

4. Install dependencies:

   ```sh
   npm ci
   ```

5. Build and run the service in development mode:

   ```sh
   make dev
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

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

### Release to testing

```sh
arc checkout -b <your-branch-name>
make patch # or minor, major
./node_modules/.bin/qtools release testing
arc pr create --push -m 'moira-int@v<your-version>'
merge pr
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

## Project Structure

```
docs            Project's public API documentation
src/            Project's source code
  app/          Application's source code
    configs     Configuration files for different environments
    v1          API handlers and libraries for version 1
    lib         Utilities and project-level libraries
  tests         Tests
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
