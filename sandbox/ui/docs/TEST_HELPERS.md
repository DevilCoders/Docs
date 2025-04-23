# Браузерные хелперы для вебдрайвера

Команды доступны в объекте `this.browser` в описаниях тестов:
```js
    this.browser
        .getRelativeUrl()
        .then(function (relativeUrl) {
            assert.equal(relativeUrl, '/tasks')
        })
```

Хелперы располагаются в директории `./path/to/root/spec/helpers/browser` и разбиты по категориям.

## Категории
* [authorization](#authorization) – работа с авторизацией на проекте;
* [browser](#browser) – расширения для методов, которые определены в вебдрайвере;
* [user](#user) – работа с пользователем;

Команды подключаются автоматически в `prepareBrowser` в `./path/to/root/.hermione.conf.js`. Любую команду можно использовать без явного подключения в каждом тесте.

## Список команд

### authorization

* [login](#login)
* [logout](#logout)
* [getLogin](#getLogin)
* [assertUserNotLoggedIn](#assertUserNotLoggedIn)

### browser

* [getRelativeUrl](#getRelativeUrl)
* [waitForAuth](#waitForAuth)

### user

* [setUser](#setUser)
* [getUser](#getUser)
* [assertUser](#assertUser)

#### login

Авторизуется с помощью переданного логина и пароля.

Текущий пользователь должен быть неавторизован.
Используется команда [waitForAuth](#waitForAuth), которая ждёт рендера блока с авторизацией на сервисе.
Авторизация проходит через `passport.yandex-team/auth`.

```js
this.browser.login(username, password)
```

Параметры:
* `username` – логин
* `password` – пароль

#### logout

Разлогинивает пользователя.

Текущий пользователь должен быть авторизован.
Используется команда [waitForAuth](#waitForAuth), которая ждёт рендера блока с авторизацией на сервисе.
Разлогин происходит на `passport.yandex-team.ru`. 
Имеется особенность, что при первом разлогине на сервисе не происходит редиректа с паспорта по `retpath` обратно на сервис, а при последующих разлогинах происходит и из-за нестабильного поведения паспорта могут некоторые тесты падать. Для таких случаев стоит `retry`.

```js
this.browser.logout()
```

#### getLogin

Возвращает логин текущего пользователя.
Вернет пустую строку для неавторизованного пользователя.

```js
this.browser
    .getLogin()
    .then(function (login) { /* ... */ })
```

#### assertUserNotLoggedIn

Проверяет, что текущий пользователь не авторизован (не залогинен).

```js
this.browser.assertUserNotLoggedIn()
```

#### getRelativeUrl

Возвращает относительный путь открытой страницы.

 ```js
this.browser
    .getRelativeUrl()
    .then(function (relativeUrl) { /* ... */ })
```

#### waitForAuth

Ожидание рендера блока авторизации, который ведёт на `passport.yandex-team.ru` на сервисе.

```js
this.browser.waitForAuth()
```

#### setUser

Авторизовывает пользователя на сервисе.
Используются авторизационные данные из `process.env` или `./path/to/root/.env`.

```js
this.browser.setUser()
```

#### getUser

Возвращает идентификатор текущего авторизованного пользователя.

```js
this.browser
    .getUser()
    .then(function (login) { /* ... */ })
```

### assertUser

Проверяет, что пользователь авторизован.
Используются авторизационные данные из `process.env` или `./path/to/root/.env`.

```js
this.browser.assertUser()
```

# Chai

Хелперы располагаются в директории `./path/to/root/spec/helpers/chai` и разбиты по категориям.

## Категории
* [assert](#assert) – расширения для `assert` методов `chai`;

## Список команд

### assert

* [batch](#batch)

#### batch

Batch-выполнение методов assert по конфигу.

```js
const assert = require('../helpers/chai/assert');

let data = '';
let expectations = {
    include: ['Task types\u000ABUILD_SANDBOX_ARCHIVE', 'Resource type'],
    notInclude: ['User groups']
};
        
assert.batch(data, expectations);
```

Параметры:
* `data` – выполняем методы над этим массивом данных
* `configs` – хеш, где `ключ` – название метода из `assert`, `значение` – массив, для каждого элемета из которого будет выполнен вызов метода   