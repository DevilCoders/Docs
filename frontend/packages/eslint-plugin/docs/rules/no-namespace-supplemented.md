# @yandex-int/no-namespace-supplemented

Расширенный вариант правила: `@react/no-namespace`.

## Options

### `namespaceAllowed`

Мы всё же хотим какие-то импорты с `*`, например:
```json
{
    "namespaceAllowed": ["React", "keyset"]
}
```
```javascript
import * as React from 'react'
import * as keyset from './Test.i18n'
```

### `exportAttention`

Ре-экспорты модулей, которые потенциально могут поехать на клиент, лучше звать точечно, а не сразу всем содержимым модуля (для случаев [доопределений и правильного организации компонент](https://github.yandex-team.ru/serp/web4/tree/dev/src/components#%D1%80%D0%B0%D1%81%D1%88%D0%B8%D1%80%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82%D0%BE%D0%B2-%D0%B8%D0%B7-%D0%BB%D0%B5%D0%B3%D0%BE) можно отключить это правило в сабмодулях).
```json
{
    "exportAttention": ["@yandex-int/serp-components", "@yandex-lego/components"]
}
```

**invalid**
```javascript
export * from '@yandex-int/serp-components/Button'
export * from '@yandex-lego/components/Icon'
```

**valid**
```javascript
export { Button } from '@yandex-int/serp-components/Button/desktop'
export { Icon } from '@yandex-lego/components/Icon/desktop'
```
