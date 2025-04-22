# yandex-logger стрим для логирования форматированным текстом

Стрим для yandex-logger, позволяющий писать в stdout отформатированную строку лога.

## Подключение

Для записи в stdout со стандартным шаблоном:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/line')()
        }
    ]
})
```

Для записи в stderr с кастомным шаблоном:

```js
const logger = require('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/qloud')({
                stream: process.stderr,
                template: '{{date}} {{msg}}\n{{err.stack}}'
            })
        }
    ]
})
```

## Шаблоны и сериализация данных

Синтаксис шаблонов похож на Mustache и поддерживает две дериктивы:

1. Вывод значения `{{name}}`, включая вложенные занчения `{{a.b.c.name}}`
2. Условные конструкции `{{#err}}Stack: {{err.stack}}{{/err}}`

В шаблоне доступны любые поля, содержащиеся в записи лога.

Чтобы правильно превратить значения поля в строку, добавлена поддержка резолверов. Работает это так:

1. Пишем в шаблонке переменную `{{date}}`
2. Добавляем в конфиге резолвер для переменной `date`:
    ```js
    const logger = require('yandex-logger')({
        streams: [
            {
                level: 'info',
                stream: require('yandex-logger/streams/qloud')({
                    stream: process.stderr,
                    template: '{{date}}',
                    resolvers: {
                        date: record => record.date.getTime()
                    }
                })
            }
        ]
    })
    ```
3. Передаем дату во время логирования: `logger.info({ date: new Date() })`
4. Получаем в логе timestamp вместо ISO Date

Резолвер по умолчанию будет прогонять значение переменной через `JSON.stringify()`.

## Пример вывода

```js
logger.info('Привет');
// out: 2018-03-21T17:21:04.665Z INFO: Привет

logger.error({
    err: new Error('Response is not valid'),
    user: { id: 123, login: 'test=user' }
}, 'Complex message with error');
// out:
// 2018-03-21T17:21:04.670Z ERROR: Complex message with error
// User: id=123; login=test-user
// Error: Response is not valid
//     at Object.<anonymous> (/Users/nodge/Sites/tools/yandex-logger/examples/entry.js:48:10)
//     at Module._compile (module.js:643:30)
//     at Object.Module._extensions..js (module.js:654:10)
```
