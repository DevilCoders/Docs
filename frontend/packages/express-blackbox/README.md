# @yandex-int/express-blackbox

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/express-blackbox/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/express-blackbox/owner.svg)

Express middleware для получения данных о пользователе из Blackbox.

## Install

```
npm install --registry=https://npm.yandex-team.ru --save @yandex-int/express-blackbox
```

## Usage

> **Pro-tip**: Для правильной работы `express-blackbox` локально необходим хост `*.yandex.*` – для этого пропишите в `/etc/hosts` строчку `127.0.0.1 local.yandex.ru` и заходите на сайт через этот адрес.

```js
const expressBlackbox = require('@yandex-int/express-blackbox');
const cookieParser = require('cookie-parser');
const express = require('express');

const app = express();

app.use(cookieParser());
app.use(expressBlackbox({ api: 'blackbox-mimino.yandex.net' }));

app.get('/', (req, res, next) => {
  console.log(req.blackbox);
  /*
	{ status: 'VALID',
	  uid: '4001209123',
	  login: 'express-blackbox',
	  displayName: 'Звездный Лорд',
	  lang: 'ru',
	  email: 'express-blackbox@yandex.ru',
	  fio: 'Блекбоксович Экспресс',
	  sex: '1',
	  country: 'ru',
	  havePassword: true,
	  haveHint: true,
	  karma: 0,
	  karmaStatus: 0,
	  raw: { blackbox response object }
	  }
	*/
});
```

Если от Черного ящика вернулась ошибка, то она тоже будет сохранена в `req.blackbox`:

```js
app.get('/', (req, res, next) => {
  console.log(req.blackbox);
  /*
	{ status: 'INVALID_PARAMS',
	  error: 'BlackBox error: Missing userip argument' }
	*/

  /*
	{ status: 'REQUEST_ERROR',
	  error: 'Response code 500 (Internal Server Error)' }
	*/
});
```

Проверка на валидность пользователя:

```js
app.get('/', (req, res, next) => {
  if (req.blackbox.status === 'VALID') {
    // ...
  }
});
```

Если вы передали дополнительные опции (такие как `aliases` или `attributes`), то их можно получить через свойство `raw`:

```js
const expressBlackbox = require('@yandex-int/express-blackbox');
const cookieParser = require('cookie-parser');
const express = require('express');

const app = express();

app.use(cookieParser());
app.use(expressBlackbox({ api: 'blackbox-mimino.yandex.net', aliases: 'all' }));

app.get('/', (req, res, next) => {
  console.log(req.blackbox.raw.aliases);
  // => { '1': 'express-blackbox' }
});
```

## API

### expressBlackbox(options)

#### options

Все параметры для [метода sessionid из Черного ящика](http://doc.yandex-team.ru/blackbox/reference/MethodSessionID.xml) передаются as-is в опциях.

##### api

_Required_
Type: `String`

Адрес [API Черного Ящика](http://doc.yandex-team.ru/blackbox/concepts/blackboxLocation.xml).

##### attributes

Type: `Object`

Поля о пользователе из `attributes`. Ключам объекта будут присвоены значения из `attributes` соответствующие значениям в `attributes`.

По умолчанию запрашиваются следующие поля:

```js
{
    login: '1008',
    fio: '1007',
    sex: '29',
    email: '14',
    country: '31',
    lang: '34',
    avatar: '98'
}
```

[Полный список](https://wiki.yandex-team.ru/passport/dbmoving/#tipyatributov) типов аттрибутов.

##### fields

Type: `Object`

Поля о пользователе из `dbfields`. Ключам объекта будут присвоены значения из `dbfields` соответствующие значениям в `fields`.

Полный список – [часто используемые данные системы авторизации](http://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/DB_About.xml).

##### phones

Type: `Object`

[Телефонные аттрибуты](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/DB_About.html#DB_About__section_kbk_b5f_2hb)

```js
{
    kind: 'all' | 'bound',
    // Ключам объекта будут присвоены значения из `attributes` соответствующие значениям в `attributes`.
    attributes: Record<string, ExpressBlackbox.PhoneAttributeKind>
}
```

##### getYaboxOptions

Type: `Function`

Способ передать в `yabox` дополнительные опции, зависящие от `req`, `res`:

```js
const expressBlackbox = require('@yandex-int/express-blackbox');

app.use(
  expressBlackbox({
    api: 'blackbox-mimino.yandex.net',
    getYaboxOptions(req) {
      return {
        query: {
          some_proxy_flag: req.query.some_proxy_flag,
        },
      };
    },
  }),
);
```

## Типовая заявка на гранты

Заявка отправляется на адрес [passport-admin@yandex-team.ru](mailto:passport-admin@yandex-team.ru)

```
Добрый день! Нам необходимы гранты для доступа к ЧЯ.

Название проекта: Мой проект (https://abc.yandex-team.ru/services/projectstub/)
Вид Черного ящика: Боевой ЧЯ / Мимино / Тестовый ЧЯ / Внутренний ЧЯ
IP-адреса компьютеров: сеть _ONLINEMEDIANETS_
Необходимые методы API Черного ящика: sessionid (https://doc.yandex-team.ru/blackbox/reference/MethodSessionID.xml)
Используемая политика защиты от подбора паролей: –
Все необходимые поля паспортной базы данных:

Аттрибуты (https://wiki.yandex-team.ru/passport/dbmoving/#tipyatributov):
	• account.default_email (14)
	• person.gender (29)
	• person.country (31)
	• person.language (34)
	• avatar.default (98)
	• person.fio (1007)
	• account.normalized_login (1008)

Необходимость обработки мобильного токена: нет

Спасибо!
```

Доступы заказываются через [Голем](https://golem.yandex-team.ru/fwreqhole.sbml).

## TVM 2

Для получения TVM тикетов можно воспользоваться мидлварой [express-tvm](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/express-tvm#express-tvm-middleware).

```js
const expressBlackbox = require('@yandex-int/express-blackbox');
const expressTvm = require('@yandex-int/express-tvm');

// Получаем тикеты и сохраняем в req.tvm
app.use(expressTvm({
  clientId: 'myapp'
	destinations: ['blackbox'],
	serverUrl: 'http://localhost:1'
	token: process.env.QLOUD_TVM_TOKEN
}));

// Используем в чёрном ящике
app.use(expressBlackbox({
	api: 'blackbox.yandex.net',
	getServiceTicket: req => {
		if (
        req.tvm &&
        req.tvm.myapp &&
        req.tvm.myapp.tickets &&
        req.tvm.myapp.tickets.blackbox
    ) {
			return req.tvm.myapp.tickets.blackbox.ticket;
		}

		// Обрабатываем ошибку по необходимости, например, так
		if (
        req.tvm &&
        req.tvm.myapp &&
        req.tvm.myapp.error
    ) {
			console.error(req.tvm.myapp.error);
		}
	}
}));
```

## OAuth

Чтобы ваше приложение умело авторизовывать пользователей по oauth токенам, необходимо зарегистрировать ваш сервис, и
создать приложение [инструкция](https://wiki.yandex-team.ru/intranet/dev/oauth/#registracijaprilozhenija)

### options

#### oauth

Type: `String|Boolean`

Значением этого параметра можно передать oauth token, или `true`,
в этом случае токен будет извлечен из заголовка `Authorization: OAuth {token}`
