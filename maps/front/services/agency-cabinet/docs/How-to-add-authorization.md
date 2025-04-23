## How to add authorization
1. Install [express-blackbox](https://github.yandex-team.ru/project-stub/express-blackbox):
```bash
npm i --save express-blackbox
```
2. Add `blackbox` section in `/configs/production.yaml`
```yaml
blackbox:
  api: blackbox.yandex.net
  regname: yes
  emails: getdefault
  fields:
    login: accounts.login.uid
    fio: account_info.fio.uid
    lang: userinfo.lang.uid
  family: 6
  aliases: 13
  timeout: 1000
```
3. Create `/server/middlewares/blackbox.js`
```js
if (process.env.MAPS_MOCKS_LOCAL) {
    module.exports = function (req, _res, next) {
        req.blackbox = {
            login: 'pupkin',
            displayName: 'Вася Пупкин',
            fio: 'Василия Васильевич Пупкин',
            uid: 15994623,
            status: 'VALID',
            raw: {
                'address-list': [{address: 'vasyapupkin@yandex.ru'}]
            }
        };
        next();
    };
} else {
    var blackboxOptions = require('../lib/config').blackbox;
    module.exports = require('express-blackbox')(blackboxOptions);
}
```
4. Create `/server/middlewares/auth.js`
```js
const config = require('../lib/config');
const logger = require('../lib/logger');

/**
 * Устанавливает данные об авторизации пользователя на основе данных из blackbox.
 */
module.exports = function (req, _res, next) {
    var blackbox = req.blackbox;
    if (blackbox.status === 'VALID' || blackbox.status === 'NEED_RESET') {
        var uid = blackbox.uid;
        var defaultEmail = blackbox.raw['address-list'][0];

        req.auth = {
            status: true,
            login: blackbox.login,
            userName: blackbox.displayName,
            uid: uid,
            fullName: blackbox.fio,
            email: defaultEmail && defaultEmail.address
        };
    } else {
        req.auth = {status: false};

        var shouldLogError = blackbox.status === 'REQUEST_ERROR' ||
            (blackbox.raw && blackbox.raw.exception && blackbox.raw.exception.value !== 'INVALID_PARAMS');
        if (shouldLogError) {
            logger.error(blackbox.error, {
                uid: req.cookies.yandexuid,
                session: req.sessionId,
                label: 'blackbox'
            });
        }
    }
    next();
};
```
5. Add these middlewares into your `/server/app.js`:
```js
const blackbox = require('./middlewares/blackbox');
const auth = require('./middlewares/auth');

app
    .use(blackbox, auth)
```

Voila! Auth and blackbox data will be available at `req.auth` and `req.blackbox`
