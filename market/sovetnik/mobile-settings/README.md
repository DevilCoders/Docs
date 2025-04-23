# Mobile settings

Sovetnik mobile settings page.

## Requirements

- [nvm](https://github.com/creationix/nvm)
- node (see version in [.nvmrc](.nvmrc))

## Setup

### Clone the repo

```sh
git clone git@github.yandex-team.ru:sovetnik/settings-mobile.git
```

### Install dependencies

```sh
cd settings-mobile
```

If you have the right version of [node](.nvmrc):

```sh
nvm use && npm i
```

If not:

```sh
nvm install <node_version_from_nvmrc_file>
npm i
```

## Build

### Development

Start local dev-server http://localhost:9000/webpack-dev-server/ with command: 
```sh
npm run serve
```

### Production
Build a package for production with command: 
```sh
npm run build
```
