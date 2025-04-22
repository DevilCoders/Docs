# Menu

<!-- description:start -->

Расширяет Menu из `lego-components`.

<!-- description:end -->

## Пример использования

```typescript jsx
import React, { FC } from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Menu as MenuBase,
  withSizeM,
  withSizeS,
  withViewPandora,
  withWidthAuto,
  withWidthMax,
  IMenuProps as IMenuDesktopProps,
} from '@yandex-int/edu-components/Menu/desktop';
import { cnTheme } from '@yandex-int/edu-components/Theme';
import { theme } from '@yandex-int/edu-components/Theme/presets/pandora-default';

interface IMenuProps extends IMenuDesktopProps {
  size?: 'm' | 's';
  view?: 'pandora';
  width?: 'auto' | 'max';
}

const Menu = compose(
  composeU(withSizeM, withSizeS),
  composeU(withWidthAuto, withWidthMax),
  withViewPandora,
)(MenuBase) as FC<IMenuProps>;

const App = () => {
  return (
    <div className={cnTheme(theme)}>
      <Menu
        disabled={false}
        size="m"
        view="pandora"
        width="max"
        items={[
          { value: 'a', content: 'Каждый' },
          { value: 'b', content: 'Охотник' },
          {
            items: [
              { value: 'c', content: 'Желает', disabled: true },
              { value: 'd', content: 'Знать' },
              { value: 'e', content: 'Где' },
            ],
          },
        ]}
        value="a"
        onChange={(event: any) => console.log(event.target.value)}
      />
    </div>
  );
};
```

## Примеры

### Внешний вид компонента

Чтобы изменить внешний вид меню, используйте модификатор `_view`.

#### pandora

{{%story::desktop:edu-components-menu-pandora--playground%}}

#### platform

{{%story::desktop:edu-components-menu-platform--playground%}}

## Свойства

> Полный список свойств см. в [Menu](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-menu-desktop--playground#свойства).

## Модификаторы

> Полный список модификаторов см. в [Menu](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Flego-components-menu-desktop--playground#модификаторы).

<!-- modifiers:start -->

### view

Задает внешний вид меню.

**Допустимые значения:** `"pandora", "platform"`.

<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Menu)
