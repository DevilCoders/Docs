[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/yandex-mailer/status.svg)](https://drone.yandex-team.ru/project-stub/yandex-mailer)

# yandex-mailer

Отправка почты через [yandex-smtp](https://wiki.yandex-team.ru/dmtdlm/javatricks/sendmail/)

## Install

```bash
npm install --save yandex-mailer
```

## Usage

```js
var mailer = require('yandex-mailer')();
var mail = {
    from: 'Яндекс <no-reply@yandex.ru>',
    to: [ 'blackheart@yandex-team.ru' ],
    subject: 'Тема письма',
    html: 'Тело письма'
};


//callback-style
function cb(err, res){};
mailer.send(mail, cb);


// promise-style
mailer.send(mail)
    .then(function(info) {
        console.info(info);
     })
     .catch(function(err) {
         console.log(err);
     })
```

## API

### mailer(options)

#### host
Type: `string`
Default: `yabacks.yandex.ru`

Хост smtp сервера

#### port
Type: `string`
Default: `25`

Порт smtp сервера


### mailer.send(mail)

#### from
Type: `string`

Отправитель

#### to
Type: `string` | `array`

Получитель

#### subject
Type: `string`

Тема письма

#### html
Type: `string`

Alias: `message_body`

Тело письма (html версия)

#### text
Type: `string`

Тело письма (plain text версия)

*Письма результата работы тестов приходят на [yandex-mailer-tests@yandex-team.ru](https://ml.yandex-team.ru/lists/yandex-mailer-tests/).*

Больше информации [тут](https://github.com/andris9/Nodemailer)
