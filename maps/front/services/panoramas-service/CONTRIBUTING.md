# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Navigate to panoramas-service project root in arcadia

   ```sh
   cd ~/arcadia/maps/front/services/panoramas-service
   ```

2. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

3. Install dependencies:

   ```sh
   make deps hosts
   ```

4. Build and run the service in development mode:

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

For run all validations use the command:

```sh
make validate
```

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools) to interface with docker, the
docker registry and the cloud platform Deploy.

### Release to testing

After the `patch/minor/major`-commit is merged into the trunk, ci runs `make release-testing`. Instead, you can do it locally.

```sh
make patch # or minor, major
arc push
```

### Deploy the current version to production

```sh
npx qtools deploy production
```

## Project Structure

```
docs            Project's public API documentation
src             Project's source code
  app           API handlers and libraries
    interfaces  App's interfaces
    middleware  Using middlewares
    lib         Utilities and project-level libraries
  tests         Tests
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
