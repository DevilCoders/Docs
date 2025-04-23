# islands-deprecated

Библиотека устаревших и малоиспользуемых блоков, удаленных из библиотеки `islands` в версии 6.0.
**Не содержит** блоков в `react`-реализации.

### Использование библиотеки

В целом библиотеку не рекомендуется использовать :) Лучше по возможности запланировать работу по переходу на актуальные блоки.

```sh
npm install --save @yandex-lego/ui.islands-deprecated --registry=https://npm.yandex-team.ru
```

### Тестирование библиотеки

Библиотека открыта для багфиксов.
Поскольку вносить изменения в `deprecated`-блоки не планируется, тесты в `ci` на них по умолчанию гоняться не будут.
Однако есть возможность включить тесты для своего PR: для этого нужно в [sandbox-ci.json](https://github.yandex-team.ru/lego/islands/blob/dev/.config/sandbox-ci.json) передать для переменной `TEST_DERPECATED` значение `1`.

### Миграция

В `meta.yml` блоков имеется краткая рекомендация по миграции. Если такая рекомендация по какой-либо причине отсутствует, а вы в ней нуждаетесь, обратитесь в наш канал [#support](https://h.yandex-team.ru/?https%3A%2F%2Flego-team.slack.com%2Fmessages%2FC0DL13NJY%2F) или напишите на рассылку [lego@yandex-team.ru](https://ml.yandex-team.ru/lists/lego/).

Вам наверняка пригодится [руководство по миграции 5.x → 6.x](https://github.yandex-team.ru/lego/islands/blob/dev/releases/6.0.0-migration.md).
