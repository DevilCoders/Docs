# @lavka/ui

## Theming

Предусмотрен механизм темизации компонентов. Есть два уровня: глобальный и локальный.

### Глобальная настройка

На уровне всего проекта можно задать тему для используемых в ней компонентах следующим образом:

```tsx
import {createTypographyStyles, createButtonStyles, defaultTypographyThemeConfig, defaultButtonThemeConfig, UikitProvider} from '@lavka/ui'
import {merge} from 'lodash-es'

/* составление темы - дефолты и кастомизация */
const theme = {
  Button: merge({}, defaultButtonThemeConfig, { /* кастомная тема для компонента Button */ }),
  Typography: defaultTypographyThemeConfig,
  /* остальные используемые компоненты */
}

/* создание css-переменных из получившейся темы */
const styles = {
  ...createButtonStyles(theme.Button),
  ...createTypographyStyles(theme.Typography),
}

const MyApp = () => {
  const i18n = useMemo(() => ({
    /* локализационные ключи */
  }), [])

  /* инжект css-переменных в head > style */
  useEffect(() => injectCss(styles), [])

  return (
    <UikitProvider i18n={i18n} theme={theme}>
      {/* компонент с приложением */}
    </UikitProvider>
  )
}
```


### Локальная настройка

Если нужно переопределить тему на уровне использования компонента, сделать это можно так:

```tsx
import {useButtonTheme, ButtonThemeConfig} from '@lavka/ui'

const customButtonTheme: ButtonThemeConfig = {
  sizes: {
    m: {
      height: 36 // переопределяем высоту кнопки размера "m"
    }
  }
}

const MyComponent = () => {
  return (
    <Button theme={customButtonTheme} size="m" variant="default">
      {/* content */}
    </Button>
  )
}
```

Динамически изменяемые конфиги темы стоит оборачивать в `useMemo`.


## Storybook

[Ссылка на внешнюю инсталляцию](https://yastatic.net/s3/grocery-superapp/storybook/v1/index.html).

Запусить локально:

```
npm run storybook
```

После запуска будет доступно по адресу `http://localhost:6006`


## Contribute

Перед тем, как добавить новый компонент, стоит посмотреть, нет ли уже такого компонента. Не всегда может быть визуально очевидно, какой компонент перед нами отображается. Визуализацию и набор свойств существующих компонентов можно посмотреть в в Storybook-e.

При разработке необходимо следовать [стайлгайду](STYLEGUIDE.md) по написанию кода.
