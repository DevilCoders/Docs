# EntityLogo

Компонент для отображения логотипа сущности.

В размере:

- `s` и `m` выводит только логотип на подложке;
- `l` под картинкой с подложкой выводится полное название из свойства `name`.

При рендеринге используется либо:

- URL картинки из полей `image.src` и опционального `image.src2x`;
- первая буква значения свойства `name`;
- значение опционального свойства `node`.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { EntityLogo as EntityLogoBase, withSizeS } from '@yandex-int/tap-components/EntityLogo';

const App: React.FC = () => {
    const EntityLogo = compose(withSizeS)(EntityLogoBase);

    return (
        <>
            <EntityLogo size="s" name="Кефир" letter="М" />
            <EntityLogo size="s" name="Молоко" />
            <EntityLogo size="s" name="Хлёб" />
        </>
    );
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-entitylogo--playground%}}

### Скелетон

{{%story:::tap-components-components-entitylogo--skeleton%}}

## Свойства

### Компонент

| Свойство      | Тип               | Описание                                            |
| ------------- | ----------------- | --------------------------------------------------- |
| className?    | `string`          | Дополнительный класс у корневого DOM-элемента       |
| image?        | `EntityLogoImage` | Картинка лого                                       |
| isExpandable? | `boolean`         | Позволяет пропорционально растягиваться             |
| letter?       | `string`          | Буква для замены логотипа, по умолчанию - `name[0]` |
| name          | `string`          | Название сущности                                   |
| node?         | `React.ReactNode` | Кастомный элемент лого                              |
| size?         | `Size`            | Размер карточки                                     |

```typescript jsx
type Size = 's' | 'm' | 'l';

type EntityLogoImage = {
    src?: string;
    src2x?: string;
};
```

### Скелетон

| Свойство      | Тип        | Описание                                      |
| ------------- | ---------- | --------------------------------------------- |
| className?    | `string`   | Дополнительный класс у корневого DOM-элемента |
| isExpandable? | `boolean`  | Позволяет пропорционально растягиваться       |
| size?         | `Size`     | Размер скелетона                              |

## CSS-переменные

| Переменная                 | Тип     | Описание                         |
| -------------------------- | ------- | -------------------------------- |
| --entity-logo-bg-color     | `color` | Цвет фона карточки-лого          |
| --entity-logo-letter-color | `color` | Цвет текста логотипа-буквы       |
| --entity-logo-name-color   | `color` | Цвет текста карточки размера `L` |
