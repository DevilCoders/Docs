# wdio-polyfill

hermione-плагин с набором полифиллов для команд браузеров. Новые версии браузеров могут удалять старую совместимость протоколов команд, что приводит к ошибкам вида `HTTP method not allowed` при использовании каких-либо команд в hermione-тестах.

## Установка

```
$ npm install @yandex-int/wdio-polyfill --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/wdio-polyfill': {
            enabled: true,
            browsers: {
                ie11: [
                    'moveTo',

                    'buttonUp',
                    'buttonDown',

                    'getValue',
                    'timeouts'
                ],
                firefox: [
                    'moveTo',

                    'buttonUp',
                    'buttonDown',

                    'getValue',
                    'getAttribute',
                    'timeouts'
                ]
            }
        }
    },

    // ...
};
```

Здесь:

- `enabled` - управляем включением плагина. По умолчанию `true`
- `browsers` - объект со списком браузеров, для которых нужно подключить полифилы
  - `browsers[commandName]` - название команды, полифил для которой нужно подключить

Весь список доступных полифилов можно посмотреть по [ссылке](lib/polyfills)
