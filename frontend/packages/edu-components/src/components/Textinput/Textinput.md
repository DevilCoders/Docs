# Textinput

<!-- description:start -->
Расширяет Textinput из `lego-components`.
<!-- description:end -->

## Пример использования

```typescript jsx
import React, { FC } from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Textinput as TextinputBase,
  withSizeM,
  withSizeS,
  withBaseline,
  withViewLyceum,
  withViewPandora,
  withReadOnly,
  ITextinputProps as ITextinputDesktopProps,
} from '@yandex-int/edu-components/Textinput/desktop';
import { cnTheme } from '@yandex-int/edu-components/Theme';
import { theme } from '@yandex-int/edu-components/Theme/presets/pandora-default';

interface ITextinputProps extends ITextinputDesktopProps {
  size?: 'm' | 's';
  view?: 'pandora' | 'lyceum';
  baseline?: boolean;
  readOnly?: boolean;
  status?: 'correct' | 'incorrect' | 'accepted';
}

const Textinput = compose(
  composeU(withViewLyceum, withViewPandora),
  composeU(withSizeM, withSizeS),
  withBaseline,
  withReadOnly,
)(TextinputBase) as FC<ITextinputProps>;

const App = () => {
  return (
    <div className={cnTheme(theme)}>
      <Textinput
        readOnly
        size="m"
        view="pandora"
        status="correct"
        placeholder="Ваш email"
        value="design@yandex-team.ru"
      />
    </div>
  );
};
```

## Примеры

### Внешний вид компонента

Чтобы изменить внешний вид текстового поля, используйте модификатор `_view`.

#### lyceum

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-textinput-lyceum--playground%}}

#### pandora

На сервисе должен быть установлен шрифт "Suisse Intl".

{{%story::desktop:edu-components-textinput-pandora--playground%}}

#### platform

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-textinput-platform--playground%}}

## Свойства

> Полный список свойств см. в [Textinput](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-textinput-desktop--playground#свойства).

## Модификаторы

> Полный список модификаторов см. в [Textinput](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-textinput-desktop--playground#модификаторы).

<!-- modifiers:start -->
### readOnly

Задает изменяемость текстового поля и добавляет ему статус.

| Свойство  | Тип                                                   | Описание                       |
| --------- | ----------------------------------------------------- | ------------------------------ |
| readOnly? | `false \| true`                                       | Состояние «только для чтения». |
| status?   | `"initial" \| "correct" \| "incorrect" \| "accepted"` | Статус текстового поля.        |

### size

Задает размер текстового поля.

**Допустимые значения:** `"l"`.

### view

Задает внешний вид текстового поля.

**Допустимые значения:** `"lyceum"`, `"pandora"`, `"platform"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Textinput)
