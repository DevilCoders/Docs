# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/creationix/nvm).

You should login to the [yandex docker registry](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
in order to be able pull and push images.

For deploying to the testing and production app clusters you will need to setup [ya](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup)
and get a token for using [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools#authorization) .

The ya tool is also used for downloading the project's secrets.

[jq](https://stedolan.github.io/jq/) utility tool is also used in some development scripts, so you'll need to have it installed.

## Getting Started

1. Go to the service folder in Arcadia

  ```sh
  cd /maps/front/services/keyserv
  ```


2. Install dependencies

  ```
  make deps
  ```

3. Add hosts

  ```
  make hosts
  ```

4. Run service

  ```
  make dev
  ```

By default http-service starts on the port `8080`.

The application can also listen on a port:

```
MAPS_NODEJS_PORT=8080 make dev
```

## Testing

To run all tests use the command:

```
make validate
make tests
```

## Deploying

This project uses [qtools](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qtools)
to interface with Deploy, Docker, Docker Registry and other cloud technologies.

```sh
make patch # or minor, major
arc pr create --push
```

Merge new PR after all checks. Pull trunk. Then create and push tag to tags/releases:
```sh
make arc-tag
```

The new arc tag will trigger a CI (Trendbox) build which:

1. Run tests.
2. Builds a docker image.
3. Pushes it to registry.
4. Deploys it to testing.

This is the preferred way to deploy.

### Manual release to testing

If CI is down, use the following steps:

```
npx qtools release testing -- --build-arg QTOOLS_TOKEN --build-arg STATIC_CLIENT_KEY
```

### Deploy the current version to production

```
npx qtools deploy production
```
