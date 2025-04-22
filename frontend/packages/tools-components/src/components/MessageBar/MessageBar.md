# MessageBar

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/MessageBar'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

Визуальный компонент, предназначенный для вывода информационных сообщений

## Пример подключения

Использование с нужным набором модификаторов:

```ts
// src/App.ts
import React from 'react'
import { compose } from '@bem-react/core'
import { withRegistry, Registry } from '@bem-react/di'

import {
  Icon as IconDesktop,
  withGlyphTypeCross,
} from '@yandex-lego/components/Icon/desktop'

import {
  withTypeWarning,
} from '@yandex-int/tools-components/Icon/desktop'

import {
  MessageBar as MessageBarDesktop,
  cnMessageBar,
  withSizeM,
  withTypeWarning,
} from '@yandex-int/tools-components/MessageBar/desktop'

const messageBarRegistry = new Registry({ id: cnMessageBar() })

const Icon = compose(withGlyphTypeCross, withTypeWarning)(IconDesktop)

messageBarRegistry
  .set('Icon', Icon)

const MessageBar = compose(
  withSizeM, 
  withTypeWarning,
  withRegistry(messageBarRegistry),
)(MessageBarDesktop)

const App = () => (
  <MessageBar 
    type="warning" 
    size="m"
    onClose={() => console.log(`Close me!`)}
  >
    MessageBar Children
  </MessageBar>
)
```

## Примеры

### Тип компонента

Чтобы изменить тип компонента, установите свойство `type` в одно из следующих значений: `"warning"`, `"info"`, `"error"`.

{{%story::desktop:tools-components-messagebar-desktop--type%}}

### Размер компонента

Чтобы изменить размер компонента, установите свойство `size` в одно из следующих значений: `"s"`, `"m"`.

{{%story::desktop:tools-components-messagebar-desktop--size%}}

### Границы

Чтобы сделать прямоугольные углы, установите свойство `pin` в значение `brick-brick`.

{{%story::desktop:tools-components-messagebar-desktop--pin%}}

## Свойства

| Свойство    | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                                                    |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------------------------------------------------------------------- |
| className?  | `string`                                                                                                                                                                                                                                                          | —            | Дополнительный className                                                    |
| onClose?    | `(event: MouseEvent<HTMLElement, MouseEvent>) => void`                                                                                                                                                                                                      | —            | Обработчик клика на close элемент и индикатор того, что close надо показать |
| hasIcon?    | `false \| true`                                                                                                                                                                                                                                                   | true         | Наличие иконки                                                              |
