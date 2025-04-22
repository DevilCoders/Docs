## How to add Uatraits
1. Install [express-http-uatraits](https://a.yandex-team.ru/arcadia/frontend/packages/express-http-uatraits):
```bash
npm i --save express-http-uatraits
```
2. Create `/server/middlewares/uatraits.js`
```js
if (process.env.MAPS_MOCKS_LOCAL) {
    module.exports = function (req, _res, next) {
        req.uatraits = {
            BrowserBase: 'Chromium',
            BrowserBaseVersion: '47.0.2526.80',
            BrowserEngine: 'WebKit',
            BrowserEngineVersion: '537.36',
            BrowserName: 'Chrome',
            BrowserVersion: '47.0.2526',
            OSFamily: 'MacOS', // 'iOS', 'Android'
            OSName: 'Mac OS X Yosemite',
            OSVersion: '10.10.5',
            isBrowser: true,
            isMobile: false
        };
        next();
    };
} else {
    module.exports = require('express-http-uatraits')();
}
```
3. Add this middleware into your `/server/app.js`:
```js
const uatraits = require('./middlewares/uatraits');

app
    .use(uatraits)
```

Voila! Uatraits data will be available at `req.uatraits`
