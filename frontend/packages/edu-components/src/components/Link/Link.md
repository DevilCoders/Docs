# Link

<!-- description:start -->
Расширяет Link из `lego-components`.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Link as LinkBase,
  withThemeNormal,
  withThemeGhost,
  withThemePseudo,
  withThemeBlack,
  withThemeOuter,
  withThemeMinor,
  withViewLyceum,
  withViewContest,
  withViewPandora,
  withPseudo,
} from '@yandex-int/edu-components/Link/desktop';

const Link = compose(
  withPseudo,
  composeU(withViewContest, withViewLyceum, withViewPandora),
  composeU(
    withThemeNormal,
    withThemeGhost,
    withThemePseudo,
    withThemeBlack,
    withThemeOuter,
    withThemeMinor,
  ),
)(LinkBase);

const App = () => {
  return (
    <Link href="/somewhere" theme="normal" view="lyceum">
      Ссылка
    </Link>
  );
};
```

## Модификаторы

<!-- modifiers:start -->
### theme

Задает стилевое оформление ссылки.

**Допустимые значения:** `"minor"`.

### view

Задает внешний вид ссылки.

Для `'lyceum'` на сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета [https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/packages/yandex-font](yandex-font).

**Допустимые значения:** `"contest"`, `"lyceum"`, `"pandora"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Link)
