# Contributing

## Requirements

* docker `>= 17.05`
* docker-compose `>= 1.23.1`

## Getting Started

```bash
nvm use

make deps
make dev.setup

make
MAPS_NODEJS_PORT=8666 make
```

## Development inside a Docker

Sometimes it might be necessary to acquire real geodata information instead of mocks locally. For this purpose you may use Docker container:

```bash
# Another OS inside of docker, better reinstall all dependencies.
rm -rf node_modules

# Prepare and start development container.
make build-docker-dev
docker-compose up -d

# Start
make docker-dev=1

# Don't forget to reinstall dependencies.
rm -rf node_modules
make deps
```

> **Notice**: Some inthosts URLs of Testing environment are not reachable inside a Docker container
> (e.g. [a `stamp.xml` for the `trf` layer](http://core-jams-rdr-cache.testing.maps.yandex.net/trf/stamp.xml)).
> Since the Tesing inthosts are used in local development you may face URL-availability issues using the Docker development.

## Testing

For run all tests use the command:

```sh
make validate
```

### Stress tests

To run all stress tests manually call:

```sh
make test-stress
```

To test specific components call:

```sh
make test-stress ARGS='-c "GET /v2"'
```

`stress` environment will be deployed automatically. Don't forget undeploy it when you finish:

```sh
make test-stress-clean
```

## Deploying

```sh
make version.patch # see mmm
arc pr create --push --publish
make version.arc-tag # see mmm

npx qtools release testing # build push and deploy
# npx qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
