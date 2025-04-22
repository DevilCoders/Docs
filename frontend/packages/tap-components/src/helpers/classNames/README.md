# classNames

Объединяет переданные классы через пробел, отфильтровывая `falsy`-значения.

## Пример использования

```typescript jsx
import { classNames } from '@yandex-int/tap-components/helpers';

const className = classNames('image', 'image_loaded', '', false, null, undefined); // 'image image_loaded'
```
