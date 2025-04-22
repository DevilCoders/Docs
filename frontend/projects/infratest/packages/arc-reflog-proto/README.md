# arc-reflog-proto

Скомпилированные proto файлы для чтения [сообщений] из [топика] на изменения серверного arc reflog из [Logbroker].

## Установка

```console
npm i @yandex-int/si.ci.arc-reflog-proto --registry=https://npm.yandex-team.ru
```

## Компиляция

Компилиция JS исходников:

```console
npm run proto
```

Компиляцию TS типов [нужно выполнять] при версии NodeJS <= 11:

```console
npm run proto:typings
```

[топика]: https://lb.yandex-team.ru/lbkx/accounts/arc/production/arcadia-reflog
[сообщений]: https://a.yandex-team.ru/arc/trunk/arcadia/arc/api/public/message.proto?rev=7248112
[Logbroker]: https://logbroker.yandex-team.ru/docs/
[нужно выполнять]: https://github.com/protobufjs/protobuf.js/issues/1222#issuecomment-500148417
