# yandex-logger стрим для логирования в Yandex.Deploy

## Подключение

Для записи в stdout:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/deploy')()
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
            stream: require('yandex-logger/streams/deploy')({ stream: process.stderr })
        }
    ]
})
```

Можно исключить из лога некоторые поля в `@fields`:
```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/deploy')({
                excludeFields: ['msg', 'msgFormat', 'msgArgs', 'level', 'levelName']
            })
        }
    ]
})
```

## Пример вывода

```js
logger.info('Привет');
// out: {"msg":"Привет","level":"INFO","levelStr":"INFO","@fields":{"pid":70489,"date":"2018-03-21T17:11:56.361Z","hostname":"nodge-osx.local","level":30,"levelName":"INFO",msgFormat":"Привет","msgArgs":[],"msg":"Привет","name":"yandex-logger"}}
```
