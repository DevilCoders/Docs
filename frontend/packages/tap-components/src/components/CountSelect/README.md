# CountSelect

Контрол выбора количества.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { CountSelect } from '@yandex-int/tap-components/CountSelect';

const App: React.FC = () => {
    const [count, setCount] = useState(1);

    return <CountSelect count={count} onChange={setCount} />;
};
```

## Пример

{{%story:::tap-components-e-commerce-countselect--playground%}}

## Свойства

| Свойство   | Тип                       | Описание                                      |
| ---------- | ------------------------- | --------------------------------------------- |
| className? | `string`                  | Дополнительный класс у корневого DOM-элемента |
| count      | `number`                  | Текущее количество                            |
| onChange   | `(count: number) => void` | Обработчик изменения количества               |

## CSS-переменные

| Переменная                               | Тип     | Описание                                       |
| ---------------------------------------- | ------- | ---------------------------------------------- |
| --count-select-action-button-bg-color    | `color` | Цвет фона основной кнопки (инкремент)          |
| --count-select-action-button-icon-color  | `color` | Цвет иконки основной кнопки (инкремент)        |
| --count-select-default-button-bg-color   | `color` | Цвет фона вспомогательной кнопки (декремент)   |
| --count-select-default-button-icon-color | `color` | Цвет иконки вспомогательной кнопки (декремент) |
