# SectionHeader

Компонент заголовка секции

## Пример использования

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';

import { SectionHeader } from '@yandex-int/tap-components/SectionHeader';

const App: React.FC = () => {
    const saleLinkComponent: React.FC = ({ children }) => (<Link to="/sale">{children}</Link>);

    return (
        <SectionHeader
            title="Распродажа"
            linkComponent={saleLinkComponent}
            linkText="Смотреть все"
        />
    );
};
```

## Пример

{{%story:::tap-components-components-sectionheader--playground%}}

## Свойства

| Свойство       | Тип                   | Описание                                                  |
| -------------- | --------------------- | --------------------------------------------------------- |
| linkComponent? | `React.ComponentType` | Компонент для создания ссылки                             |
| linkText?      | `string`              | Текст ссылки                                              |
| title?         | `string`              | Заголовок                                                 |
| titleTag?      | `React.ElementType`   | Тэг, которым будет отрисован заголовок, по умолчанию `h2` |

## CSS-переменные

| Переменная                      | Тип     | Описание    |
| ------------------------------- | ------- | ----------- |
| --section-header-link-all-color | `color` | Цвет ссылки |
