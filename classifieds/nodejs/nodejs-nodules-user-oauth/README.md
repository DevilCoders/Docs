# user-oauth

Компонент OAuth для [nodules-user].

## Использование

```js
var User = require('nodules-user'),
    OAuth = require('nodules-user-oauth');

User.registerComponent('oauth', OAuth);

// ···

var user = new User(req, res, config).init('oauth');
```

Компонент конфигурируется секцией `auth` в конфиге user.

[nodules-user]: https://github.yandex-team.ru/nodules/user
