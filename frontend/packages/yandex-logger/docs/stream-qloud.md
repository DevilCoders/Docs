# yandex-logger стрим для логирования в Qloud

Стрим для yandex-logger, позволяющий логировать в Qloud-совместимом формате.

## Подключение

Для записи в stdout:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/qloud')()
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
            stream: require('yandex-logger/streams/qloud')({ stream: process.stderr })
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
            stream: require('yandex-logger/streams/qloud')({
                excludeFields: ['msg', 'msgFormat', 'msgArgs', 'level', 'levelName']
            })
        }
    ]
})
```

## Пример вывода

```js
logger.info('Привет');
// out: {"msg":"Привет","level":"INFO","@fields":{"pid":70489,"date":"2018-03-21T17:11:56.361Z","hostname":"nodge-osx.local","level":30,"levelName":"INFO","msgFormat":"Привет","msgArgs":[],"msg":"Привет","name":"yandex-logger"}}
```
