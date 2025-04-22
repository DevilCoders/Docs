Gemini Extended Actions
=======

## Index

- [Description](#description)
- [Using](#using)
- [Custom Actions](#custom-actions)

## Description
Плагин для [Gemini](https://github.com/gemini-testing/gemini/), добавляющий возможность осуществлять дополнительные действия над браузером и вебдрайвером в процессе выполнения gemini-тестов.

## Using
Экспортируемые из плагина функции должны выполняться в контексте actions, т.е. в блоках `before`, `capture` или `after`.
Пример использования (авторизация):
```js
const utils = require('@yandex-market/gemini-extended-actions/');

gemini.suite('Suite name', function (parent) {
    parent
        .setUrl('/some/path')
        .setCaptureElements('.selector')
        .before((actions) => {
            utils.authorize.call(actions, {
                login: 'login',
                password: 'password',
                url: '/some/path'
            });
        })
        .capture('plain')
        .after((actions) => {
            utils.logout.call(actions);
        })
})

```
Либо, то же самое, но при использовании с плагином [gemini-exports](https://github.com/gemini-testing/gemini-exports):
```js
const utils = require('@yandex-market/gemini-extended-actions/');

module.exports = {
    suiteName: 'Suite name',
    url: '/some/path',
    selector: '.selector',
    before(actions) {
        utils.authorize.call(actions, {
            login: 'login',
            password: 'password',
            url: '/some/path'
        });
    },
    capture() {},
    after(actions) {
        utils.logout.call(actions);
    }
};
```

## Custom Actions

#### `authorize(options)`
Выполняет авторизацию и открывает указанную страницу

**Аргументы**
- `{String} options.login` - логин пользователя
- `{String} options.password` - пароль пользователя
- `{String} [options.url='/']` - URL, который откроем после авторизации

___

#### `logout()`
Разлогинивание путем удаления cookie `Session_id`

___

#### `openRelative(url)`
Открывает указанный url, относительно базового (указанного в конфиге gemini)

**Аргументы**
- `{String} url` - URL, который откроем
