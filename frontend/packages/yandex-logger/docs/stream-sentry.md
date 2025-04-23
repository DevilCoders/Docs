# yandex-logger стрим для логирования в Sentry

Стрим для yandex-logger, позволяющий писать логи в Sentry.

Для связи с Sentry используется [raven-node](https://github.com/getsentry/raven-node) и [got.js](https://github.com/sindresorhus/got).

## Подключение

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/sentry')({
                dsn: 'http://user:secret@localhost/2',

                // Опции будут переданы напрямую в raven-node
                clientOptions: {
                    tags: { environment: 'testing' },
                    sendTimeout: 0.5 // 500ms
                },

                // Опции будут переданы напрямую в got.js
                transportOptions: {
                    rejectUnauthorized: false
                }
            })
        }
    ]
})
```

## Поддерживаемые поля

Стрим умеет доставать из логов и отправлять в Sentry следующие поля:

* **record.name** – будет использоваться как имя логгера в Sentry
* **record.release** – передается в одноименную опцию Raven
* **record.environment** – передается в одноименную опцию Raven
* **record.tags** – список тегов для записи в Sentry
* **record.data** – передается в поле `extra` в Raven
* **record.sentry** – все свойства этого объекта будут переданы в Raven `as-is`
* **record.req** - информация о запросе, прогоняется через `raven.parsers.parseRequest`
* **record.user** - информация о пользователе, берем только `uid` и `login`

## Группировка логов

Для группировки однотипных логов можно передавать свойство `group`:
```js
const logger = require('yandex-logger')(...);

// Такая запись создаст две ранзые группы в Sentry
logger.error({ err: new Error('error-1') });
logger.error({ err: new Error('error-2') });

// А такая – одну
logger.error({ group: 'test', err: new Error('error-1') });
logger.error({ group: 'test', err: new Error('error-2') });
```

Можно воспользоваться группировкой для расклейки одинаковых записей:
```js
const logger = require('yandex-logger')(...);

// Такая запись создаст одну группу в Sentry
logger.error('test');
logger.error('test');

// А такая – две разных группы
logger.error({ group: 'test-1' }, 'test');
logger.error({ group: 'test-2' }, 'test');
```
