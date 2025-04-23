# arcanum-revision

Инструмент для работы с ревизиями в [Arcanum].

> Для идентификации большинства коммитов (commit id) Arcanum использует [хэши][commit_hash] коммитов в [arc].
Однако для идентификации коммитов из `trunk` Arcanum использует SVN-ревизии в формате `r<revision number>`.

Инструмент предоставляет методы `parse`, `format` и `isRevision`.

[Arcanum]: https://arcanum.yandex-team.ru/
[arc]: https://docs.yandex-team.ru/arc/
[commit_hash]: https://docs.yandex-team.ru/arc/ref/commands#commit-hash

## Установка

```console
$ npm i --save-prod @yandex-int/arcanum-revision
```

## Использование

```js
import ArcanumRevision from "@yandex-int/arcanum-revision";

ArcanumRevision.parse("r12345678"); // 12345678
ArcanumRevision.format(12345678);   // r12345678

ArcanumRevision.isRevision("r12345678"); // true
ArcanumRevision.isRevision("6d227551d4566dfa3a9b8c15864ec8b2f81ad24e"); // false
```
