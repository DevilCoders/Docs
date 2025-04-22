# Authorization suggestion

The site displays the authorization suggestion if the user goes to the site with a Yandex cookie. When the user presses **Continue** on a browser page, they are redirected to the OAuth authorization screen with a list of request scopes.


## Connection requirements {#requirements}

The suggestion will not work if at least one of the following conditions are met:
- The user blocked the iframe.
- The browser blocks third-party cookies.
- The user completely disabled cookies. In this case, an error will be returned when invoking [YaAuthSuggest.init](suggest.md).
- The user disabled JS.


## Before you start {#before-beginning}

Before connecting the suggestion, follow these steps:
1. Prepare the page that the suggestion will be connected to.
1. Prepare the page that will be receiving the OAuth token. The page will be displayed for a few milliseconds, so you can leave it white.
1. [Register an OAuth app](../tasks/register-client.md), if you haven't already. Add the necessary scopes to it.
1. In the registered OAuth app, select a platform in **Platforms** → **Web services**. Add the link to the page from step 2 to the **Callback URI** list.


## Connection {#connection}

After completing these steps, you can start connecting the suggestion.

Pages that will be used when connecting:
- The page that the suggestion is connected to. You need to connect the `sdk-suggest.js` script.
- Suggestion in an iframe.
- OAuth authorization.
- The page that receives the token. You need to connect the `sdk-suggest-token.js` script.


## Sdk-suggest.js script {#sdk-suggest}

Connect one of the scripts on the page where the suggestion will be placed:

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

The first script provides [polyfills](https://ru.wikipedia.org/wiki/Полифил).

### Syntax {#YaAuthSuggest-syntax}

```javascript
YaAuthSuggest.init(oauthQueryParams, tokenPageOrigin)
```

### Parameters {#YaAuthSuggest-params}

#|
|| `oauthQueryParams` | Contains the query parameters that the OAuth authorization page will be opened with:
- client_id: The [OAuth app](https://oauth.yandex.ru) ID received after registration. Required parameter.
- response_type: The request type. Required parameter.
- redirect_uri: The URI for passing the authorization result. Additional parameter. If several callback_uri are added to the app with this client_id, the user will by default be redirected to the first in the list.

See the list of all [query parameters](../reference/auto-code-client.md#auto-code-client__get-code). ||
|| `tokenPageOrigin` | The origin of the page that accepts the token and that the user will be redirected to from OAuth. Required parameter. The parameter value must always be filled in and cannot contain the `*` (asterisk) character. ||
|#

### Return value {#sdk-suggest}

The function returns a Promise, which will be allowed by the object that contains the response status, and the link to the method that opens the suggestion:

#|
|| `status` | Response status: 
- `ok`: Success.
- `error`:  Ends in an error. ||
|| `handler` | When called, returns a Promise, which opens an iframe with a suggestion when called. ||
|| `code` | Error code. String. ||
|#

### Call example {#sdk-suggest}

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
    .then(data => console.log('Message with the token', data))
    .catch(error => console.log('Processing the error', error));
```


## Sdk-suggest-token.js script {#sdk-suggest-token}

### Connection {#sdk-suggest-token}

Connect one of the scripts on the page that receives the OAuth token:

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

The first script provides [polyfills](https://ru.wikipedia.org/wiki/Полифил).

### Syntax {#YaSendSuggestToken-syntax}

```javascript
YaSendSuggestToken(origin, extraData)
```

### Parameters {#YaSendSuggestToken-params}

#|
|| `Parameters` | Origin of the page with the suggestion that a postMessage with the token will be sent to. The parameter value must always be filled in and cannot contain the `*` (asterisk) character. ||
|| `extraData` | Additional data sent to the page with the suggestion. Must be a valid JSON object. ||
|#

### Return value {#sdk-suggest-token}

The function receives information about the token from `location.search` and `location.hash` and then sends a `postMessage` with the information to the page with the suggestion and closes the current window. Doesn't return anything.

### Call example {#sdk-suggest-token}

```javascript
YaSendSuggestToken(s
    'https://example.com',
    { flag: true }
)
```

