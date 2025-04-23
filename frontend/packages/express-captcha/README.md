# express-captcha [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/express-captcha/status.svg)](https://drone.yandex-team.ru/toolbox/express-captcha)

express middleware для API Яндекс капчи

## Example

see `/example/index.js`

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install @yandex-int/express-captcha`

## Example

```js
var app = express();
var captchaOptions = {                  // << optional!
     apiHost: 'api.captcha.yandex.net', // << default: 'api.captcha.yandex.net'
     requestParameter: 'body',          // << default: 'body' for POST or 'query' for GET
     type: 'estd',                      // << default: определяем по langdetect
     vtype: 'ru',                       // << optional
     checks: 3                          // << default: 1
};

// apply middleware
app.use(express.bodyParser());
app.use(require('express-langdetect')());

app.get('/', expressCaptcha.generate(captchaOptions));
app.get('/', function (req, res) {
    if (req.captcha === null) {
        res.send(500);
        return;
    }
    res.render('download', {
        captcha: req.captcha
    });
});

app.post('/download', expressCaptcha.check(captchaOptions));
app.post('/download', function (req, res) {
    var error = req.captcha.error;
    if (error === null) {
        res.send(200, req.captcha);
    } else {
        res.send(403, req.captcha);
        // or
        // res.redirect('/?wrongCaptcha');
    }
});
```

## Типы капч `type` (русский лого | английский лого | без лого)

Если не передать параметр `type` в `expressCaptcha.generate`,
то будет использована русская капча `type=std` для локалей ru, uk, be, kk, tt и
английская капча `type=estd` для остальных языков. Вы так же можете определить тип вручную.

### обычные с циферками

```
type=std
type=estd
type=nbg
```

### с простыми циферками

```
type=lite
type=elite
type=nlite
```

### с русскими буквами

```
type=rus
нет
type=nrus
```

### с латинскими буквами (маленькими)

```
type=latl
type=elatl
tyle=nlatl
```

### с латинскими большими

```
type=latu
type=elatu
type=nlatu
```

### c латинскими смешанными

```
type=latm
type=elatm
type=nlatm
```

## Тип звуковой капчи `vtype`

Для капч типа `std`, `estd`, `nbg` возможна дополнительная генерация звуковой капчи на одном
из поддерживаемых языков: `ru`, `en`, `tr`. Если параметр не указан, то звуковая капча генерироваться не будет.

## Протокол капчи `protocol` (https | http | any)

По умолчанию протокол `any`. Будет сделан запрос к API Captcha с дополнительным параметром `?https=(on|off|any)`
в зависимости от параметра `protocol`. В ответе будет возвращена ссылка на картинку капчи с выбранным протоколом:
`https://`, `http://`, `//`.

## Количество проверок `checks`

По умолчанию количество проверок равно 1. Разрешенное количество проверок: от 0 до 9.
В случае выхода за пределы границ будет использоваться значение по умолчанию.
