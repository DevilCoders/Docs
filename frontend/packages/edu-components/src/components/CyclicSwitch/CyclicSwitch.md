# CyclicSwitch

<!-- description:start -->
Компонент для циклического переключения между вариантами.
<!-- description:end -->

## Примеры

### Пример использования

```typescript jsx
import React from 'react';
import { CyclicSwitch } from '@yandex-int/edu-components/CyclicSwitch/desktop';

const App = () => (
  <CyclicSwitch
    id="some unique id"
    options={[
      { value: '1', content: <span>1</span>, description: 'one' },
      { value: '2', content: <span>2</span>, description: 'two' },
      { value: '3', content: <span>3</span>, description: 'three' },
    ]}
    value="1"
    onChange={e => console.log(e.target.value)}
  />
);
```

## Свойства

<!-- props:start -->
| Свойство   | Тип                                                                 | По умолчанию | Описание                                                              |
| ---------- | ------------------------------------------------------------------- | ------------ | --------------------------------------------------------------------- |
| id         | `string`                                                            | —            | Уникальный идентификатор переключателя.                               |
| options    | `TSwitchOption[]`                                                   | —            | Варианты, между которыми происходит переключение.                     |
| value      | `number`                                                            | `null`       | Индекс выбранного варианта.                                           |
| onChange?  | `(e: { target: { value: number; }; }) => void`                      | —            | Обработчик, срабатывающий на переключение и передающий новый вариант. |
| disabled?  | `false \| true`                                                     | —            | Отключает интерактивность компонента.                                 |
| readOnly?  | `false \| true`                                                     | —            | Режим просмотра.<br>Компонент не дает изменять значение.              |
| innerRef?  | `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` | —            | Ссылка на корневой DOM-элемент компонента.                            |
| className? | `string`                                                            | —            | Дополнительный className.                                             |
| tabIndex?  | `number`                                                            | `0.`         | Описание отсутствует.                                                 |
| onFocus?   | `(event: FocusEvent<HTMLSpanElement>) => void`                      | —            | Обработчик события onFocus.                                           |
| onKeyDown? | `(event: KeyboardEvent<HTMLSpanElement>) => void`                   | —            | Обработчик события onKeyDown.                                         |
<!-- props:end -->

### Свойства варианта

| Свойство     | Тип       | Описание                                                                           |
| ------------ | --------- | ---------------------------------------------------------------------------------- |
| value        | `string`  | Текстовое значение варианта выбора.                                                |
| content?     | ReactNode | Визуальное представление варианта выбора. Если не передать, будет выведен `value`. |
| description? | `string`  | Описание варианта выбора. Нигде не отображается, используется для доступности.     |

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/CyclicSwitch)
