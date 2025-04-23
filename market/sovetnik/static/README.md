# Client application

> It's a new repo for our client application, the old one can be found [here](https://github.yandex-team.ru/sovetnik/sovetnik-static).

## Requirements

- [nvm](https://github.com/creationix/nvm)
- node (see version in [.nvmrc](.nvmrc))

## Setup

### Clone the repo

```console
git clone git@github.yandex-team.ru:sovetnik/static.git
```

### Install dependencies

```console
cd static
nvm use
npm i
```

## Development

### Debug chrome extension

```console
npm run dev:chrome:dbg
npm run build:chrome:dbg
npm run watch:chrome:dbg
```

### Chrome extension

```console
npm run dev:chrome
npm run build:chrome
npm run watch:chrome
```

### Run linting

```console
npm run lint
```

## Testing

Run local tests:

```console
npm t
```

## Review in web stores

### Opera Addons store

1. Prepare files

[Opera](https://wiki.yandex-team.ru/sovetnik/development/how-to/transition-from-grunt-to-npm-tasks/#opera):

```console
npm run prepare:opera
```

[Opera for distribution](https://wiki.yandex-team.ru/sovetnik/development/how-to/transition-from-grunt-to-npm-tasks/#operadistribution):

```console
npm run prepare:opera:distr
```

1. Send `opera_review.zip` and `README.md` from `build` directory to a reviewer from Opera

## Build other extensions

Please, refer to [docs](https://wiki.yandex-team.ru/sovetnik/development/how-to/transition-from-grunt-to-npm-tasks/).
