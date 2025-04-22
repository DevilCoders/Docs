# oauth-middleware

## Содержание

* [Установка](#Установка)
* [Общее описание](#Общее-описание)
* [Параметры конфигурации](#Параметры-конфигурации)
* [Использование](#Использование)
* [Public API](#API)
* [Конфигурационные переменные окружения](#Конфигурационные-переменные-окружения)
* [Дополнительно](#Дополнительно)

## Установка

```bash
npm install @yandex-int/oauth-middleware --registry=http://npm.yandex-team.ru
```

## Общее описание

`oauth-middleware` — это сервис авторизации для приложений _FEI_, реализованный в виде middleware, которая может использоваться `express` приложениями для поддержания авторизации пользователей в смежных сервисах Яндекса.

> ⚠ Middleware на запросы делегирования токенов работает только с аутентифицированные запросами, в которых есть сессионная кука в доменах `yandex-team`/`yandex`. Информацию об авторе запроса middleware получает через [blackbox].

Для того чтобы воспользоваться сервисом, необходимо проделать следующий ряд действий:

* [Зарегистрировать](https://wiki.yandex-team.ru/oauth/newservice/) свое приложение в OAuth системе
* При регистрации правильно сконфигурировать `Callback URL` с учетом того, что `<base route url>/add` обрабатывает добавление токена
* Сохранить ID и пароль приложения (например в yav). Указать их в качестве обязательных параметров конфигурации middleware: `appId` и `appSecret`
* Сгенерировать _secret passphrase_, который будет использоваться для шифрования [библиотекой crypto-js](https://cryptojs.gitbook.io/docs/#ciphers) пользовательских токенов перед сохранением в базе, и указать его в качестве обязательного параметра конфигурации: `cryptoSecret`
* [Зарегистрировать](https://wiki.yandex-team.ru/passport/tvm2/stbrief/#kakmozhnopoluchitidentifikatorservisadljatiketov) TVM приложение для своего ABC сервиса для запросов в [blackbox]
* [Заполнить](https://doc.yandex-team.ru/blackbox/tasks/HowToAccessBlackbox.html) заявку в [blackbox] для выдачи соответствующих доступов
* Для хранения токенов используется база приложения, которая использует эту middleware. В качестве `storage` при конфигурации нужно передать в параметре `collection` активного соединения клиента MongoDB.
* Сконфигурировать и подключить middleware к `express` приложению: `app.use(<route>, oauthMiddleware)` (см подробнее [использование](#Использование))

## Параметры конфигурации

Подробно интерфейс конфигурации описан в `src/types/index.ts`. Приведем описание основных параметров конфигурации:

* `appId`, `appSecret` –– ID и пароль приложения, который был зарегистрирован в [OAuth системе]
* `appSlug` –– уникальный слаг приложения. Используется для именования коллекций в общей БД (MongoDB), в которой будут храниться токены для данного приложения
* `cryptoSecret` –– любая строка, использующаяся для (де)шифрования токенов перед их сохранением в БД
* `[getRedirectUrl]` –– функция, формирующая `redirectUrl`, на который будет перенаправлен пользователь после обработки добавления токена. Функция принимает единственным параметром `state` –– десериализованный параметр, переданный в строке запроса к oauth-системе при запросе токена. (Подробнее читай [здесь](https://yandex.ru/dev/oauth/doc/dg/reference/auto-code-client.html#auto-code-client__get-code))
* `[onSuccess]` –– `callback`, срабатывающий в случае успешной обработки сохранения токена в БД (может быть асинхронным)
* `[onFailure]` –– `callback`, срабатывающий в случае ошибки во время обработки (может быть асинхронным)

После инициализации возвращается 2 объекта: `{oauthRouter, storage}` –– express router и storage, через интерфейс которого можно выполнять проверку на наличие токена, а также выдавать сам токен внутри другого приложения.

## Использование

```typescript
import express from "express";

import { configureOauthMiddleware } from "@yandex-int/oauth-middleware";

const app = express();

const APP_ID = "app-id";
const APP_SECRET = "app-secret";
const APP_SLUG = "application-slug";

const CRYPTO_SECRET = "secret";

// redirect пользователя после получения токена на страничку review request
function getRedirectUrl(state: Record<string, string>): string {
    const { rrId } = state;
    if (!rrId) {
        throw new Error(`Unexpected state arg`);
    }

    return `https://a.yandex-team.ru/review/${rrId}/details`;
}

const { oauthRouter, storage } = configureOauthRouter({
    appId: APP_ID,
    appSecret: APP_SECRET,
    appSlug: APP_SLUG,
    cryptoSecret: CRYPTO_SECRET,
    collection: db.collection("oauth-tokens"), // db => mongoDB
});


app.use("/oauth", oauthRouteMiddleware);

app.listen(80, () => console.log("Listening..."));
```

## API

* `/add?code=<oauth code>[&state=<base64 encoded json state params]>` –– обрабатывает получение токена из oauth системы и сохраняет его в БД.
* `/token?user=<login>` –– выдает токен для `user`. Запрос выполняется с авторизацией: `Authorization: Bearer <token>`. В качества `<token>` указать `appSecret` (см подробнее [Параметры конфигурации](#Параметры-конфигурации)).
* `/token/clear/all` –– удаляет из базы **ВСЕ** делегированные токены. Может использоваться в случае инвалидации всех токенов (например, при изменении скоупа доступов для токена).
* `/token/clear?user=<login>` –– удаляет из базы делегированный токен конкретного пользователя. Может использоваться в случае инвалидации токена конкретного пользователя (например, когда пользователь сам его отозвал или токен был скомпрометирован).

## Дополнительно

### Про параметр state

`state` –– это _base64_ JSON, содержащую в себе произвольные данные. Может быть использован для формирования `redirectUrl`, на который будет перенаправлен пользователь в случае успешного делегирования токена.

Пример:

```typescript
// формируется oauth системой при редиректе автоматически
const code = "12345";

const stateJson = JSON.stringify({
    rrId: "12345",
});

// формат передачи state важен: json.stringify + base64 encoding
const state = Buffer.from(stateJson).toString("base64");
```

[yandex-logger]: https://arcanum.yandex-team.ru/arc/trunk/arcadia/frontend/packages/yandex-logger
[OAuth системе]: https://oauth.yandex-team.ru
[blackbox]: https://doc.yandex-team.ru/blackbox/concepts/about.html?lang=ru
