# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses
[npm](http://npmjs.org) for tracking dependencies. It is highly recommended to develop using the
same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1). For switching quickly
between Node.js version we recommend to use [nvm](https://github.com/nvm-sh/nvm).

## Getting Started

```sh
# 1. Navigate to apikeys-int project root in arcadia
cd ~/arcadia/maps/front/services/apikeys-int
# 2. Switch to correct Node.js version
nvm use
# 3. Install dependencies and setup local development
npm ci
make dev.setup
# 4. Build project
make build # just build
make build-watch # with hot rebuild
# 5. Start service in the development mode
make dev
MAPS_NODEJS_PORT=8666 make dev # Optionally override port
```

If you are getting `RequestError: self signed certificate in certificate chain`, see [Troubleshooting](#troubleshooting)
section for a fix.

## Sending requests

```sh
# In development you can use tvmid instead of service ticket. You still can generate tickets via `ya tool tvmtool --unittest`, but why would you?
curl -H 'X-Ya-Service-Ticket: 2010470' 'http://localhost:8080/v1/check' --json '{"ip":"127.0.0.1", "key":"b027f76e-cc66-f012-4f64-696c7961c395", "counters": {"hits": 1}}'


# Update counters without checks
curl -H 'X-Ya-Service-Ticket: 2010470' 'http://localhost:8080/v1/update' --json '{"key":"69c8d500-445e-40e6-977e-64f197d2e722","counters":{"total": 1, "requests_router": 1}}'
```

## Create/update/view keys

https://wiki.yandex-team.ru/tech/developer/

| environment | admin's panel | developer's panel |
| --- | --- | --- |
| production | https://admin-developer.tech.yandex-team.ru        | https://developer.tech.yandex.ru/ |
| testing    | https://admin-developer.apikeys-pt.yandex-team.ru/ | https://developer.apikeys-pt.yandex.ru |


## Testing

```sh
make validate # single command to check everyhting below

make lint
make validate-api-doc
make test

make test MOCHA_EXTRA_OPTIONS='-g foo' # run specific tests
```

### Stress tests

```sh
make test-stress           # Run stress tests
make tests-stress-clean    # Don't forget to undeploy stress environment
```

For more information about stress testing see [src/tests/stress/README.md](src/tests/stress/README.md).

## Deploying

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the [Y.Deploy](https://deploy.yandex-team.ru/) cloud platform.

### Release

```sh
# testing
# Testing should release automatically after merge into trunk.
npx qtools release testing
# production
npx qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Checks overview

The following activity diagram shows checks which are performed for request:

![Diagram](docs/diagrams/check.png)

## Architecture overview
Recording of 64 minute post-design review (watch in 2x): [2021-01-21 apikeys-int.mp4](https://disk.yandex.ru/public/nda/?hash=FKM9FLJixAhu5Ctm61jA7Ed/WORxx7LBL878fysSe1t5Irdd7iefDFMU4k2PccsIq/J6bpmRyOJonT3VoXnDag%3D%3D)

![Overview](docs/overview/apikeys-int.png)

## Troubleshooting

### `RequestError: self signed certificate in certificate chain`

You may encounter this error when running dev server locally.

It happens because we need to access some services over HTTPS, but they are using a certificate
given by Yandex Internal Root CA.

To fix it, download `YandexInternalRootCA.crt` to your computer and add `NODE_EXTRA_CA_CERTS` to
your shell RC file (e.g. `.bashrc`):

#### Ubuntu:
```sh
# Download certificate
sudo apt-get install yandex-internal-root-ca

# Add the following line to your .bashrc
export NODE_EXTRA_CA_CERTS=/usr/share/yandex-internal-root-ca/YandexInternalRootCA.crt
```

#### MacOS:
```sh
# Download certificate
mkdir /usr/local/yandex-internal-root-ca
cd /usr/local/yandex-internal-root-ca
wget https://crls.yandex.net/YandexInternalRootCA.crt

# Add the following line to your .bashrc
export NODE_EXTRA_CA_CERTS=/usr/local/yandex-internal-root-ca/YandexInternalRootCA.crt
```

To check run: ```printenv | grep NODE_EXTRA_CA_CERTS```

More info on [wiki](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vnode.js)

Solomon signal aggregates [docs](https://wiki.yandex-team.ru/golovan/userdocs/aggregation-types)
