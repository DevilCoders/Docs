# TVM Ticket
----
[![npm version](https://badger.yandex-team.ru/npm/@yandex-market/tvm-ticket/version.svg)](https://npm.yandex-team.ru/@yandex-market/tvm-ticket)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=@yandex-market/tvm-ticket&vcs=github)](https://oko.yandex-team.ru/github/market/tvm-ticket)


Модуль для формирования подписи и параметров для запроса TVM тикета.

Поддерживаются запрос напрямую в API TVM и запрос в blackbox (ЧЯ).

* [TVM API](https://wiki.yandex-team.ru/passport/auth-tokens/using)
* [BB API](https://wiki.yandex-team.ru/passport/blackbox/#11.12.2015envsign)

## TVM API
Представлен классом `TicketRequestTvm`.
Который создается через фабрику `TvmTicket.createTicketRequest({number} clientId, {string} grantType, {number} [ts])`.

### Поддерживаемые grant_type
#### client_credentials (GRANT_TYPES.CLIENT_CREDS)

##### Свойства

* `{string} meta` или `{string} metaB64` – доп информация зашиваемая в тикет. metaB64 должно быть в base64 url-safe
* `{number} clientId` – id TVM приложения
* `{number[]} unsafeUids` – cписок небезопасных uid'ов

#### password (GRANT_TYPES.PASSWORD)

##### Свойства

* `{string} meta` или `{string} metaB64` – доп информация зашиваемая в тикет. metaB64 должно быть в base64 url-safe
* `{number} userIp` – IP адрес пользователя, если имеется. Если нет - IP адрес сервиса
* `{string} password`
* `{string} login` или `{number} uid`

#### ticket (GRANT_TYPES.TICKET)

##### Свойства

* `{string} ticket` – тикет для обновления

#### sessionid (GRANT_TYPES.SESSION_ID)

##### Свойства

* `{string} meta` или `{string} metaB64` – доп информация зашиваемая в тикет. metaB64 должно быть в base64 url-safe
* `{number} userIp` – IP адрес пользователя, если имеется. Если нет - IP адрес сервиса
* `{string} host` – хост, на который пришел пользователь с кукой
* `{string} sessionid`
* `{string} sslsessionid`


## Пример использования
```javascript
var TvmTicket = require('tvm-ticket');
var ticketRequest = TvmTicket.createTicketRequest(clientId, TvmTicket.GRANT_TYPES.CLIENT_CREDS);
// массив параметров, включая env_sign
var ticketParams = ticketRequest.getFullParams(secret);
// подпись для запроса (env_sign)
var sign = TvmTicket.sign(ticketRequest);
```

## BB API
Представлен классом `TicketRequestBb`.
Который создается через фабрику `TvmTicket.createTicketRequestBb({number} clientId, {string} method, {number} [ts])`.

### Поддерживаемые method

#### sessionid (BB_METHODS.SESSIONID)

##### Свойства

* `{string} meta` или `{string} metaB64` – доп информация зашиваемая в тикет. metaB64 должно быть в base64 url-safe
* `{number} userIp` – IP адрес пользователя, если имеется. Если нет - IP адрес сервиса
* `{string} host` – хост, на который пришел пользователь с кукой
* `{string} sessionid`
* `{string} sslsessionid`

## Пример использования

```javascript
var TvmTicket = require('tvm-ticket');
var ticketRequest = TvmTicket.createTicketRequestBb(clientId, TvmTicket.BB_METHODS.SESSIONID);
ticketRequest.host = '.yandex.ru';
ticketRequest.sessionid = '…';
ticketRequest.sslsessionid = '…';
// подпись для запроса (env_sign)
var sign = TvmTicket.sign(ticketRequest);
```
