# maps-host-configs [![build status](https://badger.yandex-team.ru/github/maps/maps-host-configs/master/state.svg)](https://github.yandex-team.ru/maps/maps-host-configs/commits/master)

Library for loading [hosts](https://github.yandex-team.ru/maps/hosts).

## Installaton

```
npm install --registry https://npm.yandex-team.ru @yandex-int/maps-host-configs
```

In addition you need to get hosts config files. For that download the following sanbox resources:

* [MAPS_CONFIG_HOSTS](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_HOSTS)
* [MAPS_CONFIG_INTHOSTS](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_INTHOSTS).

## Usage

```ts
import {createHostConfigLoader, createIntHostConfigLoader} from '@yandex-int/maps-host-configs';

// For public hosts.
const hostConfigLoader = createHostConfigLoader({
    env: process.env.QLOUD_ENVIRONMENT,
    basePath: '/path/to/hosts'
});

// For internal hosts.
const intHostConfigLoader = createIntHostConfigLoader({
    env: process.env.QLOUD_ENVIRONMENT,
    basePath: '/path/to/inthosts'
});
```

### For non-qloud users

If you don't use [Qloud](https://wiki.yandex-team.ru/qloud/) you can read environment value from special file:

1. Ensure, that debian package `yandex-environment-<env>` is installed.
2. Read environment, using:

```ts
fs.readFileSync('/etc/yandex/environment.type', 'utf8').trim();
```

See https://wiki.yandex-team.ru/development/yandex-environment/ for more information.

### Load configuration for environment

The following example loads configuration for the given environment from `<basePath>/hosts-<env>.json`:

```ts
hostConfigLoader.get().then(
    (hosts) => {
        console.log(hosts);
    },
    (error) => {
        console.error(`Failed to load hosts: ${error}`);
    }
);
```

### Apply configuration for hostname

The following example

1. Loads configuration from `<basePath>/hosts-<env>.json`
2. Extends it using values from `<basePath>/<env>/maps.yandex.ru.json` if file exists.

```ts
hostConfigLoader.get({hostname: 'maps.yandex.ru'}).then(
    (hosts) => {
        console.log(hosts);
    },
    (error) => {
        console.error(`Failed to load hosts: ${error}`);
    }
);
```

**Note:** Instead `maps.yandex.ru` can be used any valid filename, not only hostname. We call it
hostname for historical reasons. It's very similar to preset.

### Apply configuration from another hostname

The following example

1. Loads configuration from `<basePath>/hosts-<env>.json`
2. Extends it using values from `<basePath>/<env>/maps.yandex.ru.json` if file exists.
3. Extends it using values from `<basePath>/<env>/api-maps.yandex.ru.json` if file exists.

```ts
const overrides = {
    hostname: 'api-maps.yandex.ru'
};

hostConfigLoader.get({hostname: 'maps.yandex.ru', overrides}).then(
    (hosts) => {
        console.log(hosts);
    },
    (error) => {
        console.error(`Failed to load hosts: ${error}`);
    }
);
```

This functionality is needed for dynamic configuration hosts using query parameter `host_config`.
See https://st.yandex-team.ru/MAPSINFRA-25 for more information.

### Override specific hosts

**Note:** This method doesn't work in **production** environment. Mostly it's used for testing some
hosts through query parameter `host_config` without changing logic of an application.

The following example

1. Loads configuration from `<basePath>/hosts-<env>.json`
2. Extends it using values from `<basePath>/<env>/maps.yandex.ru.json` if file exists.
3. Extends it using values from `overrides.hosts`

```ts
const overrides = {
    hosts: {
        api: 'custom-api-maps.yandex.ru'
    }
};

hostConfigLoader.get({hostname: 'maps.yandex.ru', overrides}).then(
    (hosts) => {
        console.log(hosts);
    },
    (error) => {
        console.error(`Failed to load hosts: ${error}`);
    }
);
```

For internal hosts pass `overrides.inthosts` property.
