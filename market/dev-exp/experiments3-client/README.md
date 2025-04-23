# Experiments 3 NodeJS client

## [Description](https://wiki.yandex-team.ru/users/dburnazyan/texnicheskoe-reshenie-realtime-nastroek-prilozhenijj/)

### Usage example

```
const client = new ExperimentsClient({
    host: SIDECAR_HOST,
    consumer: CONSUMER_NAME,
    args: [],
    config_name: CONFIG_NAME,
});

...

client.getConfigs()
    .then((data) => {...})

Or use custom fields to override config passed to the client:

client.getConfigs({...customConfigFields})
    .then((data) => {...})

...
```
