# SearchInput

Компонент поля ввода поискового запроса.

## Пример использования

```typescript jsx
import React, { useState } from 'react';

import { SearchInput } from '@yandex-int/tap-components/SearchInput';

const App: React.FC = () => {
    const [value, setValue] = useState('');
    const onChange = event => setValue(event.target.value);
    const onSubmit = () => console.log('Search submitted!');

    return  (
        <SearchInput
            className="my-search-input"
            value={value}
            placeholder="Товар, бренд или цвет"
            hasClear
            onChange={onChange}
            onSubmit={onSubmit}
        />
    );
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-searchinput--playground%}}

### Скелетон

{{%story:::tap-components-components-searchinput--skeleton%}}

## Свойства

Основные свойства такие же, как у `Textinput`, за исключением `size` и `view` – они фиксированы.

| Свойство   | Тип          | Описание                                      |
| ---------- | ------------ | --------------------------------------------- |
| className? | `string`     | Дополнительный класс у корневого DOM-элемента |
| onSubmit?  | `() => void` | Обработчик подтверждения поиска               |

## CSS-переменные

| Переменная                       | Тип     | Описание           |
| -------------------------------- | ------- | ------------------ |
| --search-input-bg-color          | `color` | Цвет фона поля     |
| --search-input-text-color        | `color` | Цвет текста        |
| --search-input-placeholder-color | `color` | Цвет плейсхолдера  |
| --search-input-icon-color        | `color` | Цвет иконки поиска |
