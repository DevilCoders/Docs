# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Go to the project root

   ```sh
   cd <arcadia-path>/maps/front/services/{{ProjectName}}
   ```

2. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

3. Install dependencies:

   ```sh
   npm install
   ```

4. Initiate your `qtools` project by executing the ` qtools init --abc <Your ABC Service id>` command.
   This command will create the `.qtools.json` file that should be added to the repository tree.

5. Build and run the service in development mode:

   ```sh
   make
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
docker registry and the cloud platform Yandex Deploy.

### Release to testing

Just merge your PR to testing and it will be automatically deployed.

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
