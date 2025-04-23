# ecoo

Обёртка над Ecoo REST API.

## Install

```console
npm install @yandex-int/si.ci.ecoo --registry=https://npm.yandex-team.ru
```

## Usage

```js
import Client from '@yandex-int/si.ci.ecoo';

const ecoo = new Client("OAuth token");

const sign = await ecoo.createSign([1, 2, 3], 1550751829, 1000);
const stickyUrl = Client.formatStickyUrl(sign, 'https://yandex.ru');

// → https://yandex.ru/ecoo/safe/redirect?key=SOME_SIGN_HERE&to=https://yandex.ru
```

## API

### .formatStickyUrl(sign, redirectUrl, [options])

Алиас для `Client.formatStickyUrl`, доступный после инстанцирования класса.

### Client.formatStickyUrl(sign, redirectUrl, [options])

Возвращает сформированную ссылку на залипание.

> :warning: При переходе по ссылке на залипание устанавливается cookie на тот домен, с которого был произведён запрос. Например, если ссылка имеет домен `by`, то cookie ставится на домен `by`, а не какой-либо другой.

### sign

* Type: `string`

Подпись, полученная через метод `.createSign`.

### redirectUrl

* Type: `string`

Ссылка, на которую будет происходить редирект при клике на ссылку на залипание.

### options

* Type: `Object`

#### tld

* Type: `string`

Домен верхнего уровня, для которого будет установлена cookie.

#### errorUrl

* Type: `string`

Ссылка, на которую будет происходить редирект в случае ошибки при клике на ссылку на залипание.

### new Client(token, [options])

Возвращает инстанс клиента. Описание методов доступно в коде.

#### token

* Type: `string`

OAuth-токен для работы с сервисом.

#### options

* Type: [`Options`](#options-1)

Опции, используемые при инициализации клиента.

## Options

### baseUrl

* Type: `string`
* Default: `https://yandex.ru`

### retryPostMethod

* Type: `boolean`
* Default: `false`

Указывает, что POST-запросы тоже нужно ретраить.

### retryCount

* Type: `number`
* Default: `4`

Максимальное число ретраев на запрос.

### timeout

* Type: `number|undefined`
* Default: `undefined`

Время в миллисекундах, которое клиент будет ожидать ответ от сервера.

### headers

* Type: `Record<string, string>`
* Default: см. ниже

По умолчанию мы отправляем два заголовка, которые, при желании, можно заменить:

```js
{
    accept: 'application/json',
    'user-agent': '@yandex-int/si.ci.ecoo@x.x.x',
}
```

### maxRetryAfter

* Type: `number|undefined`
* Default: `undefined`

Максимальная задержка между ретраями.
