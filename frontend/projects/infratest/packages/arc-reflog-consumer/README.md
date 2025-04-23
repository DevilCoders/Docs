# arc-reflog-consumer

Пакет для обработки очереди сообщений из [топика] Logbroker по обновлению серверного рефлога.
Подробнее смотри [формат сообщений].

## Установка

```console
npm i @yandex-int/arc-reflog-consumer --registry=https://npm.yandex-team.ru
```

## Использование

```ts
import {ArcReflogConsumer, ArcReflogEvent} from "@yandex-int/arc-reflog-consumer";

const consumer = new ArcReflogConsumer({
    clientId: '<client id>',
    retryOptions: {
        forever: true,
        maxRetryTime: 4 * 3600 * 1e3,
    },
    token: '<Logbroker token>',
});

(async () => {
    await consumer.connect();

    consumer
        .on(ArcReflogEvent.FAST_FORWARD_PUSH, (data) => {});
})();
```

[топика]: https://lb.yandex-team.ru/lbkx/accounts/arc/production/arcadia-reflog
[формат сообщений]: https://a.yandex-team.ru/arc/trunk/arcadia/arc/api/public/message.proto?rev=7248112
