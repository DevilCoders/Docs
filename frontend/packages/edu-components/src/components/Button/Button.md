# Button

<!-- description:start -->
Расширяет Button из `lego-components`.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Button as ButtonBase,
  withSizeL,
  withSizeM,
  withSizeS,
  withSizeXS,
  withSizeXXS,
  withSizeXXXS,
  withViewDefault,
  withViewLyceum,
  withViewPandora,
  withThemeAction,
  withThemeClear,
  withThemePseudo,
  withThemeNormal,
  withThemeApprove,
  withThemeReject,
  withThemeGrape,
  withThemePurpleBlack,
  withThemeGrey,
} from '@yandex-int/edu-components/Button/desktop';

const Button = compose(
  composeU(withViewDefault, withViewLyceum, withViewPandora),
  composeU(
    withThemeApprove,
    withThemeReject,
    withThemeAction,
    withThemeClear,
    withThemePseudo,
    withThemeNormal,
    withThemeGrape,
    withThemePurpleBlack,
    withThemeGrey,
  ),
  composeU(withSizeM, withSizeS, withSizeXS, withSizeL, withSizeXXS, withSizeXXXS),
)(ButtonBase);

const App = () => {
  return (
    <Button size="m" theme="normal" view="lyceum">
      Кнопка
    </Button>
  );
};
```

## Модификаторы

<!-- modifiers:start -->
### size

Задает размер кнопки.

**Допустимые значения:** `"xs"`, `"xxs"`, `"xxxs"`.

### theme

Задает стилевое оформление кнопки.

**Допустимые значения:** `"approve"`, `"grape"`, `"grey"`, `"purple-black"`, `"reject"`.

### view

Задает внешний вид кнопки.

Для `'lyceum'` на сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета [https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/packages/yandex-font](yandex-font).

Для `'pandora'`на сервисе должен быть установлен шрифт "Suisse Intl".

**Допустимые значения:** `"lyceum"`, `"pandora"`, `"platform"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Button)
