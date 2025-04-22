# Styleguide

- [Styleguide](#styleguide)
  - [Файловая структура компонента](#файловая-структура-компонента)
  - [Написание стилей](#написание-стилей)
  - [Внешний className](#внешний-classname)
  - [Варианты, размеры, формы](#варианты-размеры-формы)
  - [Экспорт из библиотеки](#экспорт-из-библиотеки)
  - [Написание документации для Storybook](#написание-документации-для-storybook)
  - [Темизация компонента](#темизация-компонента)
    - [1. Описываем тип](#1-описываем-тип)
    - [2. Добавляем тип в `UikitThemeConfig`](#2-добавляем-тип-в-uikitthemeconfig)
    - [3. Описываем дефолтные значения](#3-описываем-дефолтные-значения)
    - [4. Создаем функцию конвертации темы в css-переменные](#4-создаем-функцию-конвертации-темы-в-css-переменные)
    - [5. Используем css-переменные в стилях](#5-используем-css-переменные-в-стилях)
    - [6. Для получения темы внутри компонента - `useTheme`](#6-для-получения-темы-внутри-компонента---usetheme)
    - [7. Добавляем тему в сторибук](#7-добавляем-тему-в-сторибук)
    - [8. Добавляем тему в проект](#8-добавляем-тему-в-проект)


## Файловая структура компонента

```
/MyComponent
  |- /assets - директория для хранения картинок и прочих ассетов
  |- MyComponent.tsx - код компонента
  |- MyComponent.constants.ts - используемые в разных местах константы (опционально)
  |- MyComponent.css.ts - стили
  |- MyComponent.stories.mdx - документация в сторибук
  |- MyComponent.theme.ts - описание темы при её наличии
  |- MyComponent.types.ts - общие тайпинги (опционально)
  |- index.ts - экспорт кода и тайпингов наружу
```

Если компонент имеет составные части, кладём их в отдельные директории внутри директории компонента. Структура файлов та же.

```
/MyComponent
  |- /MyComponentElement1
  |- /MyComponentElement2
```


## Написание стилей

В файле стилей `MyComponent.css.ts` пишем стили в формате

```ts
import {css} from 'linaria'

export const MyComponent = css`
  ...
`

export const someElement = css`
  ...
`
```

Далее в коде компонента используем стили

```tsx
import * as c from './MyComponent.css'

---

<div className={c.MyComponent}>
  <div className={c.someElement} />
</div>

```

## Внешний className

К корневому элементу компонента стоит всегда добавлять передаваемый снаружи `className`, который можно взять, подклеив тип `WithClassName` к пропертям компонента.

```tsx
import {cx} from 'linaria'
import {WithClassName} from '../../types'

export interface MyComponentProps extends WithClassName {
  ...
}

export const MyComponent = ({className, ...otherProps}: MyComponentProps) => {
  return (
    <div className={cx(className, c.MyComponent)} />
  )
}
```

## Варианты, размеры, формы

Если компонент имеет различные варианты, формы и размеры, то стили для них будут описаны следующим образом.

В файле типов `MyComponent.types.ts` определяем типы значений

```ts
export type MyComponentVariant = 'variant1' | 'variant2'

export type MyComponentSize = 'size1' | 'size2'
```

В файле стилей `MyComponent.css.ts` определяем

```ts
import {css} from 'linaria'

import {MyComponentVariant, MyComponentSize} from './MyComponent.types'

export const variant: Record<MyComponentVariant, string> = {
  variant1: css`...`,
  variant2: css`...`
}

export const size: Record<MyComponentSize, string> = {
  size1: css`...`,
  size2: css`...`
}

/* Если одно свойство зависит от другого */
export const variantSize: Record<MyComponentVariant, Record<MyComponentSize, string>> = {
  variant1: {
    size1: css`...`,
    size2: css`...`
  },
  variant2: {
    size1: css`...`,
    size2: css`...`
  }
}
```

В коде компонента `MyComponent.tsx` используем

```tsx
import {cx} from 'linaria'

import * as c from './MyComponent.css'
import {MyComponentVariant, MyComponentSize} from './MyComponent.types'

export interface MyComponentProps {
  variant: MyComponentVariant
  size: MyComponentSize
}

const MyComponent = ({variant, size}: MyComponentProps) => {
  return (
    <div
      className={cx(
        c.variant[variant],
        c.size[size],
        c.variantSize[variant][size]
      )}
    />
  )
}
```

## Экспорт из библиотеки

В файле `/components/index.ts` делаем экспорт нового компонента как

```ts
export * from './MyComponent'
```

Тогда в месте применения компонента можно будет импортировать его так

```ts
import {MyComponent} from '@lavka/ui'
```

## Написание документации для Storybook

При создании нового или при изменении существующего компонента необходимо поддерживать документацию в актуальном состоянии. Собирается файл `MyComponent.stories.mdx` формата MDX, который далее публикуется в сторибук.

Сначала показывается обычный компонент с таблицей пропертей

```tsx
<Canvas>
  <Story name="Default">
    {args => (
      <PreviewDecorator>
        <MyComponent {...args} />
      </PreviewDecorator>
    )}
  </Story>
</Canvas>

<ArgsTable story="Default" />
```

Чтобы компонент получил корректный контекст, его нужно рендерить в `PreviewDecorator`, а чтобы получить все возможные вариации (ru|en|he), нужно передать `theme="all"`:

```tsx
<PreviewDecorator theme="all">
  <MyComponent />
</PreviewDecorator>
```

Для правильного проставления значений по умолчанию следует делать деструктуризацию пропертей на месте аргумента функции-компонента:

```ts
const MyComponent = ({property1, property2 = 'defaultValue'}: MyComponentProps) => {
  ...
}
```

Далее можно сделать различные примеры для демонстрации различных состояний компонента.

## Темизация компонента

Тему можно добавить тогда, когда у компонента есть различия в отображении или поведении между тач и десктопной версией и не хочется каждый раз это конфигурировать через пропс компонента.

Представим, что нам нужен `Preloader`, который должен на таче иметь один цвет и размер подписи, а на декстопе другой. Чтобы каждый раз не писать `<Preloader color="..." textVariant="..." />`, можно сделать конфигурацию через тему, и задавать ее глобально один раз.

### 1. Описываем тип

```ts
// Preloader.types.ts

export interface PreloaderThemeConfig {
  color: string
  textVariant: TypographyVariant
}
```

### 2. Добавляем тип в `UikitThemeConfig`

```ts
// UikitTheme.types.ts

export interface UikitThemeConfig {
  ...
  Preloader?: PreloaderThemeConfig
  ...
}
```

### 3. Описываем дефолтные значения

```ts
// Preloader.theme.ts

export const defaultPreloaderThemeConfig: PreloaderThemeConfig = {
  color: STYLE.theme.day.text,
  textVariant: 'caption1',
}
```

### 4. Создаем функцию конвертации темы в css-переменные

```ts
// Preloader.theme.ts

export const createPreloaderStyles = (config: PreloaderThemeConfig) => {
  return {
    '--preloader-color': config.color,
  }
}
```

### 5. Используем css-переменные в стилях

```ts
// Preloader.css.ts

export const circle = css`
  color: var(--preloader-color);
`
```

### 6. Для получения темы внутри компонента - `useTheme`

```tsx
// Preloader.tsx

import {useTheme} from '../../context'

export const Preloader = () => {
  const theme = useTheme(config => config.Preloader)

  return (
    <div>
      ...
      <Typography variant={theme.textVariant}>
        ...
      </Typography>
    </div>
  )
}
```

### 7. Добавляем тему в сторибук

- [storybook-helpers/themes/ru/theme.ts](./storybook-helpers/themes/ru/theme.ts)
- [storybook-helpers/themes/en/theme.ts](./storybook-helpers/themes/en/theme.ts)
- [storybook-helpers/themes/he/theme.ts](./storybook-helpers/themes/he/theme.ts)

### 8. Добавляем тему в проект

Как темизация встраивается в проект описано в [README.md](./README.md#глобальная-настройка).

Нужно будет cконструировать необходимый объект темы, добавить ее в `<UikitProvider theme={...}>`, и заинжектить css-переменные полученные из `createPreloaderStyles` в `<style>`.
