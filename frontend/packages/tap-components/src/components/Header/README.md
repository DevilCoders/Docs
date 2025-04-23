# Header

Заголовок экрана. Позволяет вывести кнопку «Назад» и текст заголовка, в зависимости от переданных блоков.

## Пример использования

```typescript jsx
import React from 'react';
import { Header } from '@yandex-int/tap-components/Header';

const App: React.FC = () => {
    return (
        <Header
            className="my-header"
            backwardButton={<div>←</div>}
            title="Фильтры"
        />
    );
};
```

## Пример

{{%story:::tap-components-components-header--playground%}}

## Свойства

| Свойство        | Тип               | Описание                                      |
| --------------- | ----------------- | --------------------------------------------- |
| backwardButton? | `React.ReactNode` | Блок кнопки «Назад»                           |
| className?      | `string`          | Дополнительный класс у корневого DOM-элемента |
| title?          | `React.ReactNode` | Блок текста заголовка                         |

## CSS-переменные

| Переменная        | Тип     | Описание  |
| ----------------- | ------- | --------- |
| --header-bg-color | `color` | Цвет фона |
