# Spin

Индикатор загрузки. Отображает выполнение какого-то процесса, например, загрузки сайта или медиа-файла.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
  Spin as SpinBase,
  withSizeM,
  withViewDefault,
} from '@yandex-int/tap-components/Spin';

const Spin = compose(withSizeM, withViewDefault)(SpinBase)

const App: React.FC = () => (
    <Spin progress view="default" size="m" />
);
```

## Пример

{{%story:::tap-components-components-spin--playground%}}

## Свойства

| Свойство   | Тип                         | Описание                                      |
| ---------- | --------------------------- | --------------------------------------------- |
| className? | `string`                    | Дополнительный класс у корневого DOM-элемента |
| innerRef?  | `RefObject<HTMLDivElement>` | Ссылка на корневой DOM-элемент компонента     |
| progress?  | `false \| true`             | Видимость индикатора загрузки                 |
