# @yandex-lego/components &middot; ![package version](https://badger.yandex-team.ru/npm/@yandex-lego/components/version.svg)

Библиотека общих React-компонентов. Примеры и документацию см. в [Storybook](https://lego-docs.s3.mds.yandex.net/story/dev/index.html?path=/story/lego-components-button-desktop--default).

Если у вас возникли проблемы или вопросы, заходите в [раздел поддержки](https://lego.yandex-team.ru/support), спрашивайте в  [Supportboard](https://supportboard.yandex-team.ru/LEGOSUPPORT) или создайте тикет в [Startrek](https://st.yandex-team.ru/ISL) (очередь `ISL`).

## Установка

```bash
#⠀пакет с компонентами
npm i -P @yandex-lego/components --registry http://npm.yandex-team.ru
#⠀peer зависимости
npm i -P @bem-react/core @bem-react/di @bem-react/classname
```

## Использование

1. Подключите тему:

  ```ts
  // src/App.js
  import { configureRootTheme } from '@yandex-lego/components/Theme'
  import { theme } from '@yandex-lego/components/Theme/presets/default'

  // Без указания root, по умолчанию body
  configureRootTheme({ theme })
  ```

  Если на проекте есть SSR, то тему необходимо конфигурировать на сервере и подключить `SSRProvider` для синхронизации id между сервером и клиентом:

  ```ts
  // src/App.js
  import { cnTheme } from '@yandex-lego/components/Theme'
  import { theme } from '@yandex-lego/components/Theme/presets/default'
  import { SSRProvider } from '@yandex-lego/components/ssr'

  export const App = () => (
    <SSRProvider>
      <div className={cnTheme(theme)}>
        ...
      </div>
    </SSRProvider>
  )
  ```

2. Выберите сборку для использования:

  Бандл компонента со всеми модификаторами:

  ```ts
  import React from 'react'
  import { Button } from '@yandex-lego/components/Button/desktop/bundle'

  export const App = () => (
    <Button view="default" size="m">
      Button
    </Button>
  )
  ```

  Точечное подключение необходимых модификаторов:

  ```ts
  import React from 'react'
  import { compose } from '@bem-react/core'
  import { Button as ButtonDesktop, withSizeM, withViewDefault } from '@yandex-lego/components/Button/desktop'

  const Button = compose(withSizeM, withViewDefault)(ButtonDesktop)

  export const App = () => (
    <Button view="default" size="m">
      Button
    </Button>
  )
  ```

<details markdown="1">

<summary>Поддержка тем в IE11</summary>

Для поддержки тем в IE11 необходимо использовать [postcss-theme-fold](https://github.com/yarastqt/postcss-theme-fold) плагин, для того, чтобы раскрывать CSS-переменные в соответствии с темами.

**Установка:**

```bash
npm i -D postcss-theme-fold
```

**Использование:**

```js
// postcss.config.js
module.exports = {
  plugins: [
    require('postcss-theme-fold')({
      // Подключаем необходимый набор тем.
      themes: [
        [require.resolve('@yandex-lego/components/Theme/presets/default.css')],
      ],
      // Объявляем массив классов-хелперов.
      globalSelectors: ['.utilityfocus'],
    }),
  ],
}
```

</details>


## Поддерживаемые платформы

Мы поддерживаем стабильные версии всех основных браузеров, в том числе и IE11.

| Browser           | Поддерживаемая версия |
| ----------------- | --------------------- |
| Chrome            | Последние 2 версии    |
| Opera             | >= 12.1               |
| Firefox           | >= 23                 |
| Android           | >= 4                  |
| iOS Safari        | >= 5.1                |
| Internet Explorer &#42; | >= 11                 |

&#42; — требуется установка <a href="https://github.com/yarastqt/postcss-theme-fold" target="_blank">postcss-theme-fold</a> плагина.
