# tus-client

Библиотека для работы с [TUS](https://wiki.yandex-team.ru/test-user-service/).

Обратите внимание, что рекомендуемым способом взаимодействия с TUS является использование отдельного [консьюмера](https://wiki.yandex-team.ru/test-user-service/#tusconsumer). Например, [операция получения аккаунта](https://wiki.yandex-team.ru/test-user-service/#poluchenieakkaunta) невозможна без кастомного `tus_consumer`.

## Установка

```bash
$ npm install @yandex-int/tus-client --registry=http://npm.yandex-team.ru
```

## Использование

Пакет экспортирует основной класс клиента `TUSClient`, класс для ошибок `TUSError` и набор TypeScript-типов для параметров и результатов методов клиента.

### `TUSClient`

Конструктор имеет следующую сигнатуру:

```javascript
new TUSClient(OAuthToken, { tus_consumer, env }, requestsOptions)
```

`OAuthToken` - OAuth токен от TUS. В инструментах инфраструктуры использующих `tus-client`, например в [`hermione-auth-commands`](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-auth-commands), токен получается с помощью [`tokenator`](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/tokenator). При необходимости можно получить токен непосредственно к TUS ([подробности в документации](https://wiki.yandex-team.ru/test-user-service/#autentifikacija)).

По умолчанию `tus_consumer` берется равным `tus_common`, а `env` - `test`.

`requestsOptions` описывают опции по умолчанию для всех запросов. Совпадают с опциями [`si.ci.requests`](https://github.yandex-team.ru/search-interfaces/ci/tree/master/packages/requests). Могут быть переопределены на уровне отдельного запроса.

В опции [`requestsOptions.ca`](https://nodejs.org/docs/latest-v12.x/api/tls.html#tls_tls_createsecurecontext_options) по умолчанию устанавливается сертификат, получаемый с помощью пакета [`yandex-internal-cert`](../yandex-internal-cert).

Все параметры, кроме `OAuthToken`, являются опциональными.

### Поддерживаемые методы

- `createPortalAccount`
- `bindPhone`
- `getAccount`
- `unlockAccount`
- `saveAccount`
- `removeAccountFromTUS`
- `createTUSConsumer`

Сигнатура у всех методов одинаковая - `<method>(<params>, [options])`, где `params` - параметры специфичные для каждого метода и совпадающие с параметрами соответствующих методов [TUS api](https://wiki.yandex-team.ru/test-user-service/#api), а `options` - переопределения для опций [`si.ci.requests`](https://github.yandex-team.ru/search-interfaces/ci/tree/master/packages/requests).

### Пример

```typescript
import { TUSClient, CreatePortalAccountParams, CreatePortalAccountResult } from "@yandex-int/tus-client";

const client = new TUSClient("AQAD-smth");
const params: CreatePortalAccountParams = { env: "test" };
const data: CreatePortalAccountResult = await client.createPortalAccount(CreatePortalAccountParams);
/*
{
    account: {
        country: "ru",
        language: "ru",
        firstname: "test",
        lastname: "test",
        login: "y-t-login-12.34",
        password: "xyz",
        uid: "123",
    },
    passport_environment: "testing",
    saved: true,
    status: "ok",
}
*/
```

### Ошибки

Каждый метод может бросить `TUSError`, обладающую свойством `code`, которое может принимать одно из возможных значений [соответствующих кодов TUS](https://a.yandex-team.ru/arc/trunk/arcadia/passport/python/qa/test_user_service/tus_api/exceptions.py). Данная возможность может быть использована для более тонкой обработки ошибок.

```typescript
import { TUSError } from "@yandex-int/tus-client";

try {
    await client.createTUSConsumer({ env: "test" })
} catch (err) {
    if (err instanceof TUSError && err.code === "tus_consumer.already_exist") {
        // consumer уже существует, обрабатываем
    }
}
```

## e2e

```sh
npm run e2e
```

Данная библиотека поставляется с [e2e тестами](src/__e2e__/index.e2e.ts), т.е. с тестами, непосредственно взаимодействующими с TUS. Для их работы требуется [OAuth-токен от TUS](https://wiki.yandex-team.ru/test-user-service/#autentifikacija), который в тесте получается через `tokenator`.
