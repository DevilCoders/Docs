# yabox [![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/yabox/status.svg)](https://drone.yandex-team.ru/project-stub/yabox)

Обертка над [Blackbox API](http://doc.yandex-team.ru/blackbox/concepts/about.xml), возвращающая Promise с результатом.

## Install

```bash
npm install --save yabox
```

## Usage

```js
const blackbox = require('yabox')({
    api: 'blackbox.haze.yandex.net'
});

blackbox.sessionid({
    sessionid: 'getmefromusercookies'
}).then(response => {
    console.log(response.body); // => { ... }
});
```

## API

### blackbox(options)

Опции для методов blackbox.

#### options

Конкретные опции для каждого метода можно узнать в документации.

##### api
Type: `String`  

Адрес Blackbox API.

##### timeout
Type: `Number`  
Default: `500`  

Таймаут запроса в миллисекундах.

##### retries
Type: `Number`  
Default: `2`

Количество перезапросов при сетевых ошибках.

##### family
Type: `Number`  

IP address family to use when resolving host and hostname. Valid values are 4 or 6. When unspecified, both IP v4 and v6 will be used.

##### format
Type: `String`  
Default: `json`

Формат ответа Blackbox. По умолчанию `json` - будет пропущен через `JSON.parse`.

##### headers
Type: `Object`  
Default: `{}`

Заголовки, передаваемые при обращении к API.

Параметр может использоваться для передачи тикета [TVM 2](https://wiki.yandex-team.ru/passport/tvm2/).

```js
blackbox.sessionid({
    headers: { 'X-Ya-Service-Ticket': '...' }
});
```

##### agent
Type: `object`  
Default: `undefined`

HttpAgent

### blackbox.[userinfo](http://doc.yandex-team.ru/blackbox/reference/MethodUserInfo.xml)([options])

### blackbox.[sessionid](http://doc.yandex-team.ru/blackbox/reference/MethodSessionID.xml)([options])

### blackbox.[oauth](http://doc.yandex-team.ru/blackbox/reference/method-oauth.xml)([options])

### blackbox.[lcookie](https://doc.yandex-team.ru/blackbox/reference/method-lcookie.xml)([options])

### blackbox.[litesession](http://doc.yandex-team.ru/blackbox/reference/method-litesession.xml)([options])

### blackbox.[checkip](http://doc.yandex-team.ru/blackbox/reference/method-checkip.xml)([options])

### blackbox.[sign](http://doc.yandex-team.ru/blackbox/reference/method-sign.xml)([options])

### blackbox.[checksignature](http://doc.yandex-team.ru/blackbox/reference/method-checksignature.xml)([options])

### blackbox.[pwdqualit](http://doc.yandex-team.ru/blackbox/reference/method-pwdquality.xml)([options])
