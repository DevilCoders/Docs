# country-flag

React-компонент для иконок с флагами стран. Иконки загружаются c CDN.

[Список доступных флагов в svg](Flags.md)

## Установка

```bash
npm install --save @yandex-int/country-flag
```

## Использование

```jsx
import React from 'react';
import { CountryFlag } from '@yandex-int/country-flag';

export const ExampleComponent = () => {
    return (
        <CountryFlag className="example" countryCode="RU" title="Россия" />
    )
}
```
