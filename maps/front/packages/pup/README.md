# `pup`


Toolchain for testing with [Docker](https://docs.docker.com/) and [Puppeteer](https://pptr.dev/).

[Quick Start](./docs/how-to-start.md)

## Prerequisites

* node >= 8

## Installation

```
npm install --registry http://npm.yandex-team.ru --save-dev @yandex-int/pup
```

## Configuration

`pup` uses `ts` for storing its configuration. You should store the config in a file named `pup.config.ts` in the current working directory.

Create a configuration file:

```ts
const config: Config = {
    testMatch: ['<testMatch>'],
    reportPath: '<reportPath>',
    staticMocks: [],
    dynamicMocks: [],
    matchImageSnapshotOptions: {
        failureThreshold: 0.00001,
        failureThresholdType: 'percent'
    },
    timeout: 30000
};

export default config;
```

Parameters:

* `testMatch` — the glob patterns pup uses to detect test files.
* `reportPath` — the path where pup will save report.
* `staticMocks` — config for static mocks.
* `dynamicMocks` — config for dynamic mocks.
* `matchImageSnapshotOptions` — jest-image-snapshot config.
* `timeout` — timeout.

## Basic Usage

### `*, start`

Run tests.


```sh
npx pup
# or
npx pup start
```

**Options**:

* `--help` - [boolean] Show help.
* `--version` - [boolean] Show version numbe.
* `--mode` - [string] Tests run mode [choices: "play", "record", "update-snapshot"] [default: "play"]
* `--config` (`-c`) - [string] Path to config file.
* `--match` (`-m`) - [string] Match string.
* `--ci` - [boolean] Whether to run pup in continuous integration (CI) mode.
* `--standUrl` - [string] Stand url.


### `down`

Stop and remove containers, networks, images, and volumes.

```sh
npx pup down
```
