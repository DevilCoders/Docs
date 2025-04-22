# Tag

Компонент для отображения тега.

## Пример использования

### Компонент

```typescript jsx
import React from 'react';
import { Tag } from '@yandex-int/tap-components/Tag';

const App: React.FC = () => {
    return (
        <>
            <Tag active>Кроссовки</Tag>
            <Tag>Ботинки</Tag>
            <Tag>Туфли</Tag>
        </>
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { TagSkeleton } from '@yandex-int/tap-components/Tag';

const App: React.FC = () => {
    return <TagSkeleton />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-tag--playground%}}

### Скелетон

{{%story:::tap-components-components-tag--skeleton%}}

## Свойства

| Свойство       | Тип                                        | Описание                                      |
| -------------- | ------------------------------------------ | --------------------------------------------- |
| active?        | `boolean`                                  | Активен ли тег                                |
| children       | `React.ReactNode`                          | Содержимое тега                               |
| className?     | `string`                                   | Дополнительный класс у корневого DOM-элемента |
| linkComponent? | `React.ComponentType`                      | Компонент для оборачивания тега в ссылку      |
| onClick?       | `(event: MouseEvent<HTMLElement>) => void` | Обработчик нажатия на тег                     |

## CSS-переменные

| Переменная               | Тип             | Описание                     |
| ------------------------ | --------------- | ---------------------------- |
| --tag-active-bg-color    | `color`         | Цвет фона активного тега     |
| --tag-active-text-color  | `color`         | Цвет текста активного тега   |
| --tag-border-radius      | `border-radius` | Радиус скругления рамок тега |
| --tag-default-bg-color   | `color`         | Цвет фона неактивного тега   |
| --tag-default-text-color | `color`         | Цвет текста неактивного тега |
