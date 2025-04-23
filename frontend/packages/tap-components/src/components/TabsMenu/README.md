# TabsMenu

Компонент для создания горизонтального меню.

С помощью компонента можно создать:

- Статическое меню с ссылками на другие страницы.
- Меню с использованием собственного JS-кода. Например, чтобы сделать пункт меню активным.
- Переключатель для вкладок `TabsPanes`.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import {
  TabsMenu as TabsMenuBase,
  withSizeM,
  withLayoutHoriz,
  withViewDefault,
} from '@yandex-int/tap-components/TabsMenu';

const TabsMenu = compose(
  withSizeM,
  withViewDefault,
  withLayoutHoriz,
)(TabsMenuBase);

const App: React.FC = () => {
  const [activeTab, setActiveTab] = useState('tab1');

  return (
    <TabsMenu
      size="m"
      view="default"
      layout="horiz"
      activeTab={activeTab}
      tabs={[
        { id: 'tab1', onClick: () => setActiveTab('tab1'), content: 'Tab 1' },
        { id: 'tab2', onClick: () => setActiveTab('tab2'), content: 'Tab 2' },
      ]}
    />
  )
}
```

## Пример

{{%story:::tap-components-components-tabsmenu--playground%}}

## Свойства

| Свойство   | Тип                           | Описание                                      |
| ---------- | ----------------------------- | --------------------------------------------- |
| activeTab? | `string`                      | Идентификатор активного пункта меню           |
| tabs       | `ITabsMenuTabProps[]`         | Массив пунктов меню                           |
| innerRef?  | `RefObject<HTMLUListElement>` | Ссылка на корневой DOM-элемент компонента     |
| className? | `string`                      | Дополнительный класс у корневого DOM-элемента |
