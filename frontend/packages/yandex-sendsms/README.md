# yandex-sendsms

Отправка sms через [YaSMS](https://doc.yandex-team.ru/Passport/YaSMSDevGuide/concepts/About.xml)

## Install

```bash
npm install --save yandex-sendsms
```

## Usage

Вызов методов API
```javascript
var yasms = require('yandex-sendsms')(options);

yasms[method](data)
    .then(function(res) {
        console.info(res);
    })
    .catch(function(err) {
        console.error(err);
    });
```

Отправка СМС
```javascript
var yasms = require('yandex-sendsms')();

yasms.sendsms({
        sender: 'promopages',
        identity: 'mobile',
        text: 'yandex-sendsms test',
        phone: '+79999999999'
    })
    .then(function(res) {
        console.info(res);
    })
    .catch(function(err) {
        console.error(err);
    });
```

### YaSMS(options)
type: `Object`

#### protocol
Type: `String`

Default: `'http'`

Протокол YaSMS сервера

#### host
Type: `String`

Default: `'sms.passport.yandex.ru'` в `production` окружении, `'phone-passport-test.yandex.ru'` в других окружениях

Хост YaSMS сервера

#### timeout
Type: `Number`

Default: `2000`

Таймаут ответа ручки в миллисекундах

#### parse
Type: `Boolean`

Default: `true`

Парсить ли xml-ответ ручки

### API

Все вызовы методов возвращают промисы

```
sendsms(data)
userphones(data)
checksms(data)
register(data)
confirm(data)
```

[Список методов и их параметров](https://doc.yandex-team.ru/Passport/YaSMSDevGuide/concepts/YaSMS_Main.xml#api)
