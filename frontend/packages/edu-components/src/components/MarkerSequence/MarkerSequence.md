# MarkerSequence

<!-- description:start -->
Компонент для задач со списком произвольных элементов.
<!-- description:end -->

## Примеры

### Пример использования

```tsx
import React, { useCallback } from 'react';
import { compose, composeU } from '@bem-react/core';
import { Registry, withRegistry } from '@bem-react/di';

import {
  MarkerSequence as MarkerSequenceBase,
  cnMarkerSequence,
} from '@yandex-int/edu-components/MarkerSequence/desktop';

type TTextInputProps = {
  id: string;
  value: any;
  disabled: boolean;
  readOnly: boolean;

  onChange: (id: string, value: any) => void; // eslint-disable-line @typescript-eslint/no-explicit-any
};

const TextInput: FC<TTextInputProps> = ({ id, value, disabled, readOnly, onChange }) => {
  const handleChange = useCallback(e => onChange(id, e.target.value), [id, onChange]);

  return (
    <div>
      <input
        type="text"
        style={style}
        value={value}
        disabled={disabled}
        readOnly={readOnly}
        onChange={handleChange}
      />
    </div>
  );
};

const AddButton = ({ onAdd }) => <button onClick={onAdd}>add</button>;
const RemoveButton = ({ id, onRemove }) => <button onClick={() => onRemove(id)}>x</button>;

const markerSequenceRegistry = new Registry({ id: cnMarkerSequence() });

markerSequenceRegistry.set('AddButton', AddButton);
markerSequenceRegistry.set('RemoveButton', RemoveButton);

const MarkerSequence = compose(withRegistry(markerSequenceRegistry))(MarkerSequenceBase);

// Используем в приложении
const App = () => (
  <MarkerSequence
    value={[]}
    minLength={4}
    maxLength={7}
    renderItem={params => <TextInput {...params} />}
    onChange={value => console.log(value)}
    onRemove={id => console.log('remove', id)}
    onAdd={() => console.log('add new item')}
  />
);
```

## Свойства

<!-- props:start -->
| Свойство   | Тип                                        | По умолчанию | Описание                                                                                                                |
| ---------- | ------------------------------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| value      | `TValue[]`                                 | —            | Массив значений.                                                                                                        |
| statuses?  | `any[]`                                    | `[]`         | Массив статусов.                                                                                                        |
| className? | `string`                                   | —            | Дополнительный класс.                                                                                                   |
| innerRef?  | `RefObject<HTMLDivElement>`                | —            | Ссылка на корневой DOM-элемент.                                                                                         |
| disabled?  | `false \| true`                            | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                 |
| readOnly?  | `false \| true`                            | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно. |
| minLength? | `number`                                   | `0`          | Минимальное количество элементов.                                                                                       |
| maxLength? | `number`                                   | `100`        | Максимальное количество элемментов.                                                                                     |
| renderItem | `(params: TRenderItemParams) => ReactNode` | —            | Render prop для отрисовки элемента.                                                                                     |
| onChange?  | `(value: TValue[]) => void`                | —            | Обработчик изменения значения.                                                                                          |
| onRemove?  | `(id: string) => void`                     | —            | Обработчик на удаление элемента.                                                                                        |
| onAdd?     | `() => void`                               | —            | Обработчик на добавление элемента.                                                                                      |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### layout

Задает расположение вариантов ответа.

**Допустимые значения:** `"horizontal"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerSequence)
