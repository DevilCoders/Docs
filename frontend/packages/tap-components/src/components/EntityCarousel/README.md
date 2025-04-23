# EntityCarousel

Компонент карусели сущностей.

## Пример использования

```typescript jsx
import React from 'react';
import { EntityCarousel } from '@yandex-int/tap-components/EntityCarousel';

const App: React.FC = () => {
    const allLinkComponent: React.FC = ({ children }) => (<a href="ya.ru">{children}</a>);

    return (
        <EntityCarousel
            entities={entities}
            allLinkComponent={allLinkComponent}
            texts={{ title: 'Заголовок' }}
            className="my-entity-carousel"
        />
    );
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-entitycarousel--playground%}}

### Скелетон

{{%story:::tap-components-components-entitycarousel--skeleton%}}

## Свойства

### Компонент

| Свойство          | Тип                   | Описание                                                     |
| ----------------- | --------------------- | ------------------------------------------------------------ |
| allLinkComponent? | `React.ComponentType` | Компонент для формирования ссылки на страницу всех сущностей |
| allLinkText?      | `Texts`               | Текст для ссылки на все элементы карусели                    |
| className?        | `string`              | Дополнительный класс у корневого DOM-элемента                |
| entities          | `Array<EntityData>`   | Данные о сущностях                                           |
| title?            | `React.ReactNode`     | Заголовок карусели                                           |

```typescript jsx
type EntityData = {
    entity: EntityLogo;
    linkComponent?: React.ComponentType;
}
```

### Скелетон

| Свойство    | Тип        | Описание                                       |
| ----------- | ---------- | ---------------------------------------------- |
| className?  | `string`   | Дополнительный класс у корневого DOM-элемента  |
| count?      | `number`   | Количество скелетонов элементов карусели       |
| withTitle?  | `boolean`  | Отвечает за отрисовку скелетона заголовка      |

## CSS-переменные

### Компонент

| Переменная                         | Тип      | Описание                                                              |
| ---------------------------------- | -------- | --------------------------------------------------------------------- |
| --entity-carousel-link-all-color   | `color`  | Цвет ссылки на страницу всех сущностей                                |
| --entity-carousel-side-indent      | `px`     | Величина, на которую нужно "вытащить" блок из родителя слева и справа |

### Скелетон

| Переменная                                | Тип      | Описание                                                              |
| ----------------------------------------- | -------- | --------------------------------------------------------------------- |
| --entity-carousel-skeleton-side-indent    | `px`     | Величина, на которую нужно "вытащить" блок из родителя слева и справа |
| --entity-carousel-skeleton-title-height   | `px`     | Высота скелетона заголовка                                            |
| --entity-carousel-skeleton-title-margin   | `margin` | Внешние отступы скелетона заголовка                                   |
