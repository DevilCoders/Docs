# Cаджест авторизации

Саджест авторизации отобразится на сайте, если пользователь переходит на сайт с cookie Яндекса. Когда пользователь нажмет на странице браузера **Продолжить**, он будет переадресован на экран OAuth-авторизации с перечнем скоупов для запроса.

## Требования к подключению {#requirements}

Если выполнен хотя бы один из следующих пунктов, то саджест не будет работать:
 
- Пользователь запретил открытие iframe.
- Браузер блокирует сторонние cookie.
- Пользователь полностью отключил cookie. В этом случае при вызове [YaAuthSuggest.init](#YaAuthSuggest-syntax) вернется ошибка.
- Пользователь отключил JS.

## Перед началом {#before-beginning}

Перед подключением саджеста выполните шаги:
 
1. Подготовьте страницу, на которую будет подключен саджест.
1. Подготовьте страницу, которая будет принимать OAuth-токен. Страница будет отображаться несколько миллисекунд, поэтому можно оставить белый экран.
1. [Зарегистрируйте OAuth-приложение](../tasks/register-client.md), если вы еще этого не сделали. Добавьте в него необходимые скоупы.
1. В зарегистрированном OAuth-приложении, включите галочку в разделе. Добавьте в список **Callback URI** ссылку на страницу из пункта 2.

## Подключение {#connection}

После выполнения этих пунктов можно начать подключение саджеста.

Страницы, которые будут использоваться при подключении:
 
- Страница, на которую подключается саджест. Необходимо подключить скрипт `sdk-suggest.js`.
- Саджест в iframe.
- OAuth-авторизация.
- Страница, принимающая токен. Необходимо подключить скрипт `sdk-suggest-token.js`.

## Скрипт sdk-suggest.js {#sdk-suggest}

Подключите один из скриптов на странице, где будет размещен саджест:

```html
<head>
    <script src="https://yastatic.net/s3/passport-sdk/autofill/v1/sdk-suggest-with-polyfills-latest.js"></script>
</head>
```

```html
<head>
    <script src="https://yastatic.net/s3/passport-sdk/autofill/v1/sdk-suggest-latest.js"></script>
</head>
```

Первый скрипт предоставляет [полифилы](https://ru.wikipedia.org/wiki/Полифил).

### Синтаксис {#YaAuthSuggest-syntax}

```javascript
YaAuthSuggest.init(oauthQueryParams, tokenPageOrigin)
```

### Параметры {#YaAuthSuggest-params}

#|
|| `oauthQueryParams` | Cодержит query-параметры, с которыми будет открыта страница OAuth-авторизации:
* `client_id` — идентификатор [OAuth-приложения](https://oauth.yandex.ru/), который был получен после регистрации. Обязательный параметр.
* `response_type` — тип запроса. Обязательный параметр.
* `redirect_uri` — URI для передачи результата авторизации. Дополнительный параметр. Если в приложение с данным `client_id` добавлено несколько `callback_uri`, тогда по умолчанию произойдет редирект на первый из них.

См. список всех [query-параметров](../reference/auto-code-client.md#get-code). ||
|| `tokenPageOrigin`	| 	Origin страницы, которая принимает токен и на которую произойдет редирект с OAuth. Обязательный параметр. Значение параметра должно быть всегда заполнено и не содержать символ * (звездочка). ||
|#

### Возвращаемое значение {#sdk-suggest-return-value}

Функция возвращает Promise, который будет разрешен объектом, содержащим статус ответа, и ссылку на метод, открывающий саджест:

#|
|| `status` |
Статус ответа:
* `ok` — успешен.
* `error` — завершен ошибкой. 
||
|| `handler`	| 	При вызове возвращает Promise, который при вызове открывает iframe с саджестом. ||
|| `code`	| 	Код ошибки. Строка. ||
|#

### Пример вызова {#sdk-suggest-call-example}

```javascript
YaAuthSuggest.init(
    {
        client_id: 'c46f0c53093440c39f12eff95a9f2f93',
        response_type: 'token',
        redirect_uri: 'https://example.com/suggest/token'
    },
    'https://example.com'
)
    .then(({handler}) => handler())
    .then(data => console.log('Сообщение с токеном', data))
    .catch(error => console.log('Обработка ошибки', error));
```

## Скрипт sdk-suggest-token.js {#sdk-suggest-token}

### Подключение {#sdk-suggest-token-connect}

Подключите один из скриптов на странице, принимающей OAuth-токен:

```javascript
<head>
    <script src="https://yastatic.net/s3/passport-sdk/autofill/v1/sdk-suggest-token-with-polyfills-latest.js"></script>
</head>
```

```javascript
<head>
    <script src="https://yastatic.net/s3/passport-sdk/autofill/v1/sdk-suggest-token-latest.js"></script>
</head>
```

Первый скрипт предоставляет [полифилы](https://ru.wikipedia.org/wiki/Полифил).

### Синтаксис {#YaSendSuggestToken-syntax}

```javascript
YaSendSuggestToken(origin, extraData)
```

### Параметры {#YaSendSuggestToken-params}

#|
|| `origin`	| 	Origin страницы с саджестом, на которую будет отправлен `postMessage` с токеном. Значение параметра должно быть всегда заполнено и не содержать символ * (звездочка). ||
|| `extraData`	| 	Дополнительные данные, отправляемые на страницу с саджестом. Должен быть валидным JSON-объектом. ||
|#

### Возвращаемое значение {#sdk-suggest-token-return-value}

Функция получает информацию о токене из `location.search` и `location.hash`, а затем отправляет `postMessage` с информацией на страницу с саджестом и закрывает текущее окно. Ничего не возвращает.

### Пример вызова {#sdk-suggest-token-call-example}

```javascript
YaSendSuggestToken(
    'https://example.com',
    { flag: true }
)
```