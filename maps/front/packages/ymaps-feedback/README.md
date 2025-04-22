# ymaps-feedback

Node.js модуль для отправки отзывов на Яндекс картах.


## Установка

```
npm install --registry http://npm.yandex-team.ru ymaps-feedback
```

Если вы используете данный модуль внутри Qloud, то включите NAT64 в сетевых настройках вашего окружения.

## Подключение
TS
```ts
import {sendMail} from 'ymaps-feedback';
```

JS
```js
const {sendMail} = require('ymaps-feedback');
```

## API

### sendMail

```ts
function sendMail(options: object): Promise<void>
```

Отправляет отзыв через сервис [yabacks](https://wiki.yandex-team.ru/yaback/). Перед отправкой отзыв проходит проверку через сервис [спамообороны](https://wiki.yandex-team.ru/AlexMart/FormsSpamCheck).

Пример:

```js
var feedback = require('ymaps-feedback');

feedback.sendMail({
    family: 6,
    feedbackOptions: {
        subject: 'Feedback about beta.maps.yandex.ru',
        recipientEmail: 'support@maps.yandex.ru'
    },
    spamCheckOptions: {
        serviceUrl: 'http://so1h-dev.mail.yandex.net:80/',
        ip: '84.201.173.29',
        host: 'beta.maps.yandex.ru',
        realpath: '/',
        formName: 'maps'
    },
    userHeaders: {
        'x-otrs-maps': '',
        'x-otrs-maps-content': ''
    }
}).then(
    function () {
        console.log('Thanks for your feedback!');
    },
    function (error) {
        console.error(error);
    }
);
```

#### Проверка на спам

Вне зависимости от результатов проверки на спам письмо отправляется. При этом в заголовки запроса добавляются результаты проверки на спам.

| Заголовок       | Принимаемое значение | Описание |
| -----------     | ------------         | ---------  |
| X-SO-Spam-uid   | {Number}             | Уникальный идентификатор сообщения |
| X-SO-Spam-Flag  | YES                  | Сообщение расценено как спам |
|                 | NO                   | Сообщение не определено как спам |
|                 | UNDEF                | Не удалось определить (см. X-SO-Spam-check) |
| X-SO-Spam-check | OK                   | Получен ответ от спамобороны |
|                 | REQUEST_TIMEOUT      | Превышено время ожидания ответа от спамобороны |
|                 | IS_DISABLED          | Проверка спама отключена |
|                 | ERROR                | Спамоборона не ответила или формат ответа не соответствует ожидаемому |

#### Формат письма

Текст отправляемого письма имеет следующий формат:

* текст сообщения
* основные поля `fields`
* разделитель
* дополнительные поля `additionalFields` - эти поля не видны пользователю при ответе и содержат служебную информацию, например, содержимое user agent.

Пример:

```
Текст сообщения пользователя

permalink: beta.maps.yandex.ru

----
email: user@exmaple.com
name: user name
browser: firefox
```

Принятый формат нужен для правильной обработки в ОТРС (таск-трекер для службы поддержки), подробности можно узнать у alkvi@.

## Запуск тестов

```
npm install
npm test
```
