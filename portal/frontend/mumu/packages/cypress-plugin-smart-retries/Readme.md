Этот плагин делает две вещи:
1. добавляет случайную задержку 1-1.5 секунды между ретраями (по умолчанию тесты ретраятся со скоростью света, что не очень хорошо при проблемах с сетью/стендом)
2. добавляет дополнительные ретраи, если тест (или before/after хук) упали с ошибкой, подходящей под шаблон

**Важно:** из-за особенности реализации можно добавить экстра ретрай только если ещё остались не израсходованые обычные ретраи.

## Установка

1. `npm i --save-dev @yandex-int/cypress-plugin-smart-retries`

2. Добавьте в support/index.ts
```ts
import {smartRetries} from '@yandex-int/cypress-plugin-smart-retries';

smartRetries({
    maxExtraRetries: 10, // Сколько ретраев нужно добавить
    errorPatterns: [ // На каких ошибках надо добавлять ретраи
        'We received this error at the network level',
        'This was considered a failure because the status code was not `2xx`'
    ]
});

```
