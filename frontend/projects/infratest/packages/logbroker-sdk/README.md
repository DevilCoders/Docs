# logbroker-sdk

SDK представляет собой верхнеуровневый интерфейс для [записи][Logbroker/write] и [чтения][Logbroker/read] сообщений в [Logbroker].

> :warning: Настоятельно рекомендуется сначала ознакомиться с документацией [Logbroker].

## Поддержка

За помощью можно обращаться на рассылку [infraduty@].

## Установка

```console
npm i @yandex-int/si.ci.logbroker-sdk --registry=https://npm.yandex-team.ru
```

## API
### Класс `Reader`
#### Конструктор

Создаёт объект для чтения данных, в качестве параметра принимает объект с полями:
*  `proxyHostname`: имя хоста, полный список приведён в [документации][Logbroker/clusters];
*  `topics`: название топика, можно указывать сразу несколько названий;
*  `clientId`: название клиента, от имени которого будет осуществляться чтение;
*  `grpcOptions`: объект для расширения дефолтных настроек подключения по gRPC;
*  `credentials`: oAuth токен. О том как получить токен, читайте в [документации][Logbroker/oauth];

Полный набор параметров описан в интерфейсе [`ReadSettings`][package-types].

:warning: На данный момент SDK не умеет авторизоваться через TVM.

```typescript
import { Reader } from "@yandex-int/si.ci.logbroker-sdk";

const GRPC_OPTIONS = {
    "grpc.keepalive_time_ms": 20000,
    "grpc.keepalive_timeout_ms": 20000,
    "grpc.keepalive_permit_without_calls": 1,
};

const reader = new sdk.Reader({
    proxyHostname: 'lbkx.logbroker.yandex.net',

    topics: ['some/logbroker/topic'],
    clientId: 'some/logbroker/clientId',

    grpcOptions: GRPC_OPTIONS,

    credentials: '<TOKEN>',
});
```

#### Метод `connect`
Инициализирует и устанавливает сессию чтения с автоматически выбранным хостом кластера. Возвращает поток, который расширяет стандартный Duplex Stream событиями "error", "commit" и "message".

Метод инкапсулирует следующие шаги:
* https://logbroker.yandex-team.ru/docs/concepts/data/read/#discovery
* https://logbroker.yandex-team.ru/docs/concepts/data/read/#init

##### События
###### Событие `error`
В чтец можно добавить свои обработчики ошибок, как сделано, например, в пакете [@yandex-int/arc-reflog-consumer].

```typescript
const stream = await reader.connect();

stream.on("error", (error: ConsumerError) => {
    handleError(error);
});
```

###### Событие `commit`
Выбрасывается, когда хост подтвердил, что получил от чтеца запрос `Commit`. Запрос отправляется методом `commitMessage`.

```typescript
const stream = await reader.connect();

// Чтец получил порцию данных из хоста, обработал и подтвердил.
stream.on("commit", async () => {
    // Идём за следующей порцией данных
    await reader.readNextMessage();
});
```

###### Событие `message`
Выбрасывается, когда получили результат чтения. Аргументом событие является объект типа `ConsumerData`.

```typescript
const stream = await reader.connect();

stream.on("message", async (data: ConsumerData) => {
    const { cookie = null } = data;
    const { messageBatch: batch = [] as Array<ConsumerMessageBatch> } = data;

    for (const batchData of batch) {
        const { message: messages = [] as Array<ConsumerMessage> } = batchData;

        for (const message of messages) {
            processMessage(message);
        }
    }

    if (cookie) {
        await reader.commitMessage([cookie]);
    }
});
```

#### Метод `commitMessage`

После обработки результата чтения клиент подтверждает серверу получение запросом `Commit`, содержащим поле `cookie`.
`cookie` — один или более токенов для подтверждения прочтения, полученных в результатах чтения.

```typescript
const stream = await reader.connect();

// Необходимые cookie передаются хостом в событие message.
await reader.commitMessage([cookie]);
```

#### Метод `readNextMessage`
Отправляет запрос `Read` на чтение следующей порции данных. В качестве параметра принимает объект с полями:
* `maxCount`: ограничение максимального количества сообщений в результате чтения;
* `maxSize`: ограничение максимального размера результата чтения в байтах.

Поля необязательны, полный набор параметров описан в интерфейсе `NPersQueue.ReadRequest.IRead`.

Метод инкапсулирует следующие шаги:
* https://logbroker.yandex-team.ru/docs/concepts/data/read/#read

```typescript
const stream = await reader.connect();

await reader.readNextMessage({
    // Читать по 10 сообщений за один сетевой запрос.
    maxCount: 10
});
```

### Пример простого чтеца

```typescript
import { Reader } from "@yandex-int/si.ci.logbroker-sdk";

const GRPC_OPTIONS = {
    "grpc.keepalive_time_ms": 20000,
    "grpc.keepalive_timeout_ms": 20000,
    "grpc.keepalive_permit_without_calls": 1,
};

const reader = new sdk.Reader({
    proxyHostname: 'lbkx.logbroker.yandex.net',

    topics: ['some/logbroker/topic'],
    clientId: 'some/logbroker/clientId',

    grpcOptions: GRPC_OPTIONS,

    credentials: '<TOKEN>',
});

const stream = await reader.connect();

stream.on("error", async (error: ConsumerError) => {
    await handleError(error);
});

stream.on("commit", async () => {
    await reader.readNextMessage();
});

stream.on("message", async (data: ConsumerData) => {
    const { cookie = null } = data;
    const { messageBatch: batch = [] as Array<ConsumerMessageBatch> } = data;

    for (const batchData of batch) {
        const { message: messages = [] as Array<ConsumerMessage> } = batchData;

        for (const message of messages) {
            processMessage(message);
        }
    }

    if (cookie) {
        await reader.commitMessage([cookie]);
    }
});

await reader.readNextMessage({
    maxCount: 10,
});
```

### Примеры
#### Пакеты
* [@yandex-int/si.ci.arcanum-consumer]
* [@yandex-int/arc-reflog-consumer]

#### Чтецы
* [cmnt-node]
* [devexp]


### Класс `Writer`

> :warning: Класс Writer у нас нигде не используется и не был протестирован в бою, используйте на свой страх и риск.

#### Конструктор

Создаёт объект для записи данных, в качестве параметра принимает объект с полями:
*  `proxyHostname`: имя хоста, полный список приведён в [документации][Logbroker/clusters];
*  `topics`: название топика, можно указывать сразу несколько названий;
*  `sourceId`: идентификатор [группы сообщений][Logbroker/message-group];
*  `grpcOptions`: объект для расширения дефолтных настроек подключения по gRPC;
*  `credentials`: oAuth токен. О том как получить токен, читайте в [документации][Logbroker/oauth];

Полный набор параметров описан в интерфейсе [`WriteSettings`][package-types].

:warning: На данный момент SDK не умеет авторизоваться через TVM.

#### Метод `write`

Отправляет запрос `Write` на запись данных. В качестве параметра принимает буфер, который может быть [protobuff] сообщением или простым текстом.

Метод инкапсулирует следующие шаги:
* https://logbroker.yandex-team.ru/docs/concepts/data/write#write


[infraduty@]: mailto:infraduty@yandex-team.ru

[Logbroker]: https://logbroker.yandex-team.ru/docs/
[Logbroker/oauth]: https://logbroker.yandex-team.ru/docs/concepts/security#oauth
[Logbroker/clusters]: https://logbroker.yandex-team.ru/docs/concepts/clusters_and_installations#installations_list
[Logbroker/message-group]: https://logbroker.yandex-team.ru/docs/concepts/resource_model#message-group
[Logbroker/read]: https://logbroker.yandex-team.ru/docs/concepts/data/read
[Logbroker/write]: https://logbroker.yandex-team.ru/docs/concepts/data/write
[package-types]: src/types/client.ts
[protobuff]: https://developers.google.com/protocol-buffers

[@yandex-int/si.ci.arcanum-consumer]: https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/arcanum-consumer
[@yandex-int/arc-reflog-consumer]: https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/arc-reflog-consumer
[cmnt-node]: https://github.yandex-team.ru/cmnt/cmnt-node/blob/2fc391916bd297e1c61f57bc4faf3cf6b783c37f/src/app/logbroker.ts
[devexp]: https://github.yandex-team.ru/devexp/devexp/blob/bc7b197425243079471e2bfc48c6bc9b57e63fa6/src/services/arc/logbroker-reader/class.js
