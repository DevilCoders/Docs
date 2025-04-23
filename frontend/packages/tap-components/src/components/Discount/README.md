# Discount

Скидка на товар.

## Пример использования

```typescript jsx
import React from 'react';
import { Discount } from '@yandex-int/tap-components/Discount';

const App: React.FC = () => {
    return <Discount className="my-discount" discount="-35%" />;
};
```

## Пример

{{%story:::tap-components-e-commerce-discount--playground%}}

## Свойства

| Свойство   | Тип      | Описание                                      |
| ---------- | -------- | --------------------------------------------- |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |
| discount   | `string` | Сообщение о скидке                            |


## CSS-переменные

| Переменная          | Тип     | Описание  |
| ------------------- | ------- | --------- |
| --discount-bg-color | `color` | Цвет фона |
