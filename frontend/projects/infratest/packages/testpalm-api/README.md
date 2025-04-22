# @yandex-int/testpalm-api

> Клиент для работы с TestPalm API.

## Установка

```console
npm install @yandex-int/testpalm-api --registry=https://npm.yandex-team.ru
```

## Использование

### Текущее API

```ts
import Client from "@yandex-int/testpalm-api";

const client = new Client("OAuth token");

(async () => {
    const testCases = await client.getTestCases("serp-js", {
        include: ["id", "name"]
    });
})();
```

### Старое API

Описание старого клиента для устаревающего API вынесено в [отдельный файл](./old-client.md).

```js
const { OldClient } = require("@yandex-int/testpalm-api");

const client = new Client();
```

## API

### new Client(token, [options])

#### token

* Type: `string`

OAuth-токен для работы с сервисом. [Процесс получения](https://wiki.yandex-team.ru/testpalm/testpalmdoc/api/).

#### options

* Type: [`Options`](#options-1)

Опции, используемые при инициализации клиента.

## Options

### baseUrl

* Type: `string`
* Default: `https://testpalm-api.yandex-team.ru`

### retryPostMethod

* Type: `boolean`
* Default: `false`

Указывает, что POST-запросы тоже нужно ретраить.

### retryPatchMethod

* Type: `boolean`
* Default: `false`

Указывает, что PATCH-запросы тоже нужно ретраить. Этот сетевой метод используется при обновлении тест-кейсов.

### retryCount

* Type: `number`
* Default: `3`

Максимальное число ретраев на запрос.

### headers

* Type: `Record<string, string>`
* Default: см. ниже

По умолчанию мы отправляем два заголовка, которые, при желании, можно заменить:

```js
{
    accept: "application/json",
    "user-agent": "testpalm-api",
}
```

### maxRetryAfter

* Type: `number|undefined`
* Default: `undefined`

Максимальная задержка между ретраями.

## Фильтрация и гранулярное получение данных

Каждый GET-метод имеет дополнительный аргумент `query`, в который передаётся объект, декларирующий фильтрацию на стороне TestPalm.
