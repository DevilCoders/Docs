# Select

<!-- description:start -->
Расширяет Select из `lego-components`.
<!-- description:end -->

## Пример использования

Селект состоит из триггера (кнопки), попапа, меню и иконки.

### Button.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import {
  Button as ButtonBase,
  withSizeM,
  withViewPandora,
  withBaseline,
  withWidthMax,
  IButtonProps as IButtonDesktopProps,
} from '@yandex-int/edu-components/Button/desktop';

export interface IButtonProps extends IButtonDesktopProps {
  width: 'max';
  baseline?: boolean;
  view?: 'pandora';
  size?: 'm';
}

export const Button = compose(
  withWidthMax,
  withBaseline,
  withViewPandora,
  withSizeM,
)(ButtonBase) as FC<IButtonProps>;
```

### Popup.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import {
  Popup as PopupBase,
  withTargetAnchor,
  withViewPandora,
  IPopupProps as IPopupDesktopProps,
} from '@yandex-int/edu-components/Popup/desktop';
import { withZIndex } from '@yandex-lego/components/withZIndex';

export interface IPopupProps extends IPopupDesktopProps {
  view?: 'pandora';
}

export const Popup = compose(
  withTargetAnchor,
  withViewPandora,
  withZIndex,
)(PopupBase) as FC<IPopupProps>;
```

### Menu.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import {
  Menu as MenuBase,
  withSizeM,
  withViewPandora,
  withWidthMax,
  IMenuProps as IMenuDesktopProps,
} from '@yandex-int/edu-components/Menu/desktop';

export interface IMenuProps extends IMenuDesktopProps {
  size?: 'm';
  view?: 'pandora';
  width?: 'max';
}

export const Menu = compose(
  withSizeM,
  withViewPandora,
  withWidthMax,
)(MenuBase) as FC<IMenuProps>;
```

### Icon.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose, withBemMod } from '@bem-react/core';
import {
  Icon as IconBase,
  IIconProps as IIconCommonProps,
  cnIcon,
} from '@yandex-lego/components/Icon/desktop';

export interface IIconProps extends IIconCommonProps {
  glyph?: 'carets-v';
}

export const withGlyphCaretsV = withBemMod<{}, IIconProps>(
  cnIcon(),
  { glyph: 'carets-v' },
  Icon => ({ className, ...props }) => (
    <Icon {...props} className={cnIcon({ hasGlyph: true }, [className])}>
      <svg width="12" height="12" xmlns="http://www.w3.org/2000/svg">
        <path
          fillRule="evenodd"
          clipRule="evenodd"
          d="M1.76 5l2.828 2.828 1.415 1.415 1.414-1.415L10.245 5 8.831 3.586 6.003 6.414 3.174 3.586 1.76 5z"
        />
      </svg>
    </Icon>
  ),
);

// Иконка должна быть обёрнута с модификатор с глифом `carets-v`
export const Icon = compose(withGlyphCaretsV)(IconBase) as FC<IIconProps>;
```

### Textinput.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import {
  Textinput as TextinputBase,
  ITextinputProps as ITextinputDesktopProps,
  withSizeM,
  withViewPandora,
  withBaseline,
  withReadOnly,
} from '@yandex-int/edu-components/Textinput/desktop';

interface ITextinputProps extends ITextinputDesktopProps {
  size?: 'm';
  view?: 'pandora';
  baseline?: boolean;
  readOnly?: boolean;
  status?: 'correct' | 'incorrect' | 'accepted';
}

export const Textinput = compose(
  withSizeM,
  withViewPandora,
  withBaseline,
  withReadOnly,
)(TextinputBase) as FC<ITextinputProps>;
```

### Select.tsx

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import { Registry, withRegistry } from '@bem-react/di';
import { withOutsideClick } from '@yandex-lego/components/withOutsideClick';
import { withTogglable } from '@yandex-lego/components/withTogglable';
import {
  Select as SelectBase,
  cnSelect,
  withBaseline,
  withViewPandora,
  withReadOnly,
  withWidthSynced,
  ISelectProps as ISelectPropsDesktop,
} from '@yandex-int/edu-components/Select/desktop';

import { Button } from './Button';
import { Menu } from './Menu';
import { Popup, IPopupProps } from './Popup';
import { Icon } from './Icon';
import { Textinput } from './Textinput';

// Создаём адаптер для попапа.
// По умолчанию попап в селекте не рендерится до его открытия.
// Через forceRender сможем синхронизировать кнопку и попап по ширине.
const MountedPopup: FC<IPopupProps> = props => <Popup forceRender {...props} />;

const registry = new Registry({ id: cnSelect() })
  // Оборачиваем попап в `withOutsideClick`, если нужно, чтобы он закрывался по клику вовне
  .set('Popup', withOutsideClick(MountedPopup))
  .set('Trigger', Button)
  .set('Menu', Menu)
  .set('Icon', Icon)
  // Textinput станет триггером в режиме readonly
  .set('Textinput', Textinput);

export interface ISelectProps extends ISelectPropsDesktop {
  size?: 'm';
  view?: 'pandora';
  baseline?: boolean;
  readOnly?: boolean;
  status?: 'correct' | 'incorrect' | 'accepted';
  width?: 'synced';
}

export const Select = compose(
  withRegistry(registry),
  withViewPandora,
  withReadOnly,
  withTogglable,
  withBaseline,
  withWidthSynced,
)(SelectBase) as FC<ISelectProps>;
```

### App.tsx

```typescript jsx
import React from 'react';
import { configureRootTheme } from '@yandex-int/edu-components/Theme';
import { theme } from '@yandex-int/edu-components/Theme/presets/pandora-default';

import { Select } from './Select';

// Конфигурация темы на уровне проекта
configureRootTheme({ theme });

const App = () => {
  return (
    <Select
      baseline
      readOnly
      status="correct"
      width="synced"
      size="m"
      view="pandora"
      value="a"
      options={[
        { value: 'a', content: 'Раз' },
        { value: 'b', content: 'Два' },
        { value: 'c', content: 'Три' },
      ]}
    />
  );
};
```

## Примеры

### Внешний вид компонента

Чтобы изменить внешний вид селекта, используйте модификатор `_view`.

#### pandora

На сервисе должен быть установлен шрифт "Suisse Intl".

{{%story::desktop:edu-components-select-pandora--playground%}}

#### platform

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-select-platform--playground%}}

## Свойства

> Полный список свойств см. в [Select](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-select-desktop--playground#свойства).

## Модификаторы

> Полный список модификаторов см. в [Select](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-select-desktop--playground#модификаторы).

<!-- modifiers:start -->
### readOnly

Задает изменяемость селекта и добавляет ему статус.

| Свойство  | Тип                                                   | Описание                        |
| --------- | ----------------------------------------------------- | ------------------------------- |
| readOnly? | `false \| true`                                       | Сделать ли селект неизменяемым. |
| status?   | `"initial" \| "correct" \| "incorrect" \| "accepted"` | Статус селекта.                 |

### view

Задает внешний вид селекта.

**Допустимые значения:** `"pandora"`, `"platform"`.

### width

Задает ширину селекта по самому длинному пункту меню (desktop-only).

**Допустимые значения:** `"synced"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Select)
