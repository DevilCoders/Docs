# yandex-logger стрим для логирования в json

Стрим для yandex-logger, позволяющий писать в stdout простой json.

## Подключение

Для записи в stdout:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/json')()
        }
    ]
})
```

Для записи в stderr:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/json')({ stream: process.stderr })
        }
    ]
})
```

Для записи в файл:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/json')({
                stream: requrie('fs').createWriteStream('/dev/null')
            })
        }
    ]
})
```

## Пример вывода

```js
logger.info('Привет');
// out: {"pid":70296,"date":"2018-03-21T17:08:49.542Z","hostname":"nodge-osx.local","level":30,"levelName":"INFO","msgFormat":"Привет","msgArgs":[],"msg":"Привет","name":"yandex-logger"}
```
