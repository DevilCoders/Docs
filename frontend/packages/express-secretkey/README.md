# express-secretkey [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/express-secretkey/status.svg)](https://drone.yandex-team.ru/toolbox/express-secretkey) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/express-secretkey&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/express-secretkey)

Middleware для генерации и валидации CSRF-токенов.

> Спецификация — http://doc.yandex-team.ru/XScript5/interface-developer-guide/concepts/secret-key.xml

## Usage

```js
var app = express();

// Подключение зависимостей
app.use(express.cookieParser());
app.use(require('express-blackbox')());
app.use(require('express-yandexuid')());

var secretkey = require('express-secretkey')();

// Генерация токена
app.use(secretkey);

app.get('/', function (req) {
    console.log(req.secretkey);
});

// Валидация токена
app.post('/', secretkey.validate, function (req) {
    console.log('token is valid');
});
```

## API

### Secretkey(options)

Создаёт middleware.

#### options

Type: `Object`

Объект с опциями.

##### ignoreMethods

Type: `Array`
Default: `['GET', 'HEAD', 'OPTIONS']`

Массив `HTTP`-методов, для которых не будет проверяться токен.

##### version

Type: `Number`
Default: `1`

Номер версии [@yandex-int/secret-key](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/secret-key).

##### salt

Type: `String`

Фраза свободного формата. Является необходимым параметром, если используется `version: 2`.

##### lifetime

Type: `Number`
Default: `1000 * 60 * 60 * 24`

Время жизни токена в миллисекундах. Используется, если указана `version: 2`.

##### timestamp

Type: `Number`
Default: `Date.now()`

Таймстемп генерации ключа. Используется, если указана `version: 2`.

##### value

Type: `Function`
Default:

```js
function (req) {
  return (req.body && req.body.sk)
    || (req.query && req.query.sk)
    || (req.headers['csrf-token'])
    || (req.headers['xsrf-token'])
    || (req.headers['x-csrf-token'])
    || (req.headers['x-xsrf-token']);
}
```

Функция, определяющая способ получения CSRF-токена из объекта `request`.

### secretkey(req, res, next)

Добавляет CSRF-токен в поле `secretkey` объекта `request`.

### secretkey.validate(req, res, next)

Валидирует CSRF-токен, полученный из объекта `request`.
