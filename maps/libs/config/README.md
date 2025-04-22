# maps/libs/config

This library allows to read config files that depend on the environment.

## ya.make resources:

The config files are fetched from resources where keys are equal to the config file locations in the old scheme, like /etc/yandex/maps/router.json

1. Create library containing config files as resources.
2. Resource keys should be similar to paths where these configs were installed previously.
3. Use `maps/libs/config` to retrieve config file by path. This library will look up the current environment and return the correct config file.

Rules for matching are the following:

* config file for `unittest` enviroment, if the binary was executed by `ya make -t`,
* config file for environment name defined in `ENVIRONMENT_NAME` environment variable, if it is set,
* config file for environment name defined in /etc/yandex/environment.name,
* config file for environment name defined in /etc/yandex/environment.type,
* config file for environment name defined in /etc/yandex/environment.alias,
* config file for `default` environment,
* exact match,
* exact match for the file on filesystem.

First match wins and if there is no match, an exception is thrown.

## How to use
Add `PEERDIR(maps/libs/config)` in your `ya.make`. The library contains only one function:

```(cpp)
maps::config::readConfigFile(const std::string& configPath);
```
