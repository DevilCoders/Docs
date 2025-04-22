# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

## Getting Started

1. Go to the project root

   ```sh
   cd <arcadia-path>/maps/front/services/geodisplay-int
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

### How to get Debug User Ticket for local development

1. Run `make build dev` to start the app and the tvmtool daemon.
2. Get an [OAuth token](https://oauth.yandex.ru/authorize?response_type=token&client_id=be4044964e7243f4b6dd1b6785e78cd3) and export it as `DEBUG_USER_TICKETS_TOKEN` environment variable:
```sh
export DEBUG_USER_TICKETS_TOKEN=<token>
```
3. To get a user ticket and print it to stdout, run:
```sh
make dev.get-debug-user-ticket
```
4. Or you can use it together with `curl` like this:
```sh
curl -H "X-Ya-User-Ticket: $(make dev.get-debug-user-ticket)" "http://localhost:8080/v1/stub_endpoint"
```

## Testing

For run all tests use the command:

```sh
make validate
```

## Work with database

To setup database for local development see [README.md](../../tools/mmm/README.md#work-with-database) in `mmm` tool.

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools) to interface with docker, the
docker registry and the cloud platform Yandex Deploy.

### Release to testing

Just merge your PR to testing and it will be automatically deployed.

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```

## Authentication

In testing and dev environments we use blackbox-mimino. Grants:
* Testing
  * https://st.yandex-team.ru/PASSPORTGRANTS-9322
  * https://st.yandex-team.ru/PASSPORTGRANTS-9494
* Prod
  * TODO

## Troubleshooting

### macOS and make errors
If you're using macOS and when running any make target you encounter errors, see the [troubleshooting section](../../tools/mmm/README.md#troubleshooting) in `mmm` tool.

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
