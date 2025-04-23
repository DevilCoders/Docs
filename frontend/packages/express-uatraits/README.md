# express-uatraits

Определение устройства, используя uatraits.

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install @yandex-int/express-uatraits`

## Example

```js
// install
app.use(require('express-uatraits')({
    browser: '/usr/share/uatraits/browser.xml',
    profiles: '/usr/share/uatraits/profiles.xml',
    extra: '/usr/share/uatraits/extra.xml' // опционально
}));

// use

app.get('/', function (req) {
    console.log(req.uatraits);
});
```
