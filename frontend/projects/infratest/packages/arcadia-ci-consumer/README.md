# arcadia-ci-consumer

Пакет для обработки очереди сообщений из [топика] Logbroker обо всех событиях, происходящих с flow.
Подробнее смотри [формат сообщений].

## Установка

```console
npm i @yandex-int/si.ci.arcadia-ci-consumer --registry=https://npm.yandex-team.ru
```

## Использование

```ts
import { ArcadiaCiConsumer, ArcadiaCiEventType } from "yandex-int/si.ci.arcadia-ci-consumer";

const consumer = new ArcadiaCiConsumer({
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
        .on(ArcadiaCiEventType.ET_FINISHED, (data)) => {});
})();
```

[топика]: https://logbroker.yandex-team.ru/lbkx/accounts/ci/events/stable
[формат сообщений]: https://a.yandex-team.ru/svn/trunk/arcadia/ci/proto/event/event.proto?rev=r9021492
