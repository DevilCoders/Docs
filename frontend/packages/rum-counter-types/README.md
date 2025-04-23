# rum-counter-types

TypeScript типы для пакета [@yandex-int/rum-counter](https://github.yandex-team.ru/RUM/rum-counter).

## Установка

Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-int/rum-counter-types --scope=<package-name>
```
где `<package-name>` - название пакета, куда нужно установить `rum-counter-types`.

Пример использования:
```typescript jsx
/// <reference types="@yandex-int/rum-counter-types" />

import '@yandex-int/rum-counter/dist/bundle/send';
import '@yandex-int/rum-counter/dist/bundle/implementation';
```
