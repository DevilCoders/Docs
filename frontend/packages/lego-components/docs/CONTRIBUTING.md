# Разработка

Установите все зависимости в корне монорепозитория и в пакете `packages/lego-components`.

```bash
npm ci
```

## Сборка проекта

```bash
npm run build
```

## Сборка документации для Storybook

Для сборки документации используется пакет [ts-docgen](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/packages/ts-docgen).

```bash
npm run docs
```

## Сборка документации для сайта

Документация для сайта собирается автоматически через `ts-docgen-loader` и компонент `<PropsTable />`

1. Создайте файл props.tsx в папке `docs` для компонента. В который нужно импортировать все необходимые типы и из которого нужно экспортировать по дефолту компонент. Cодержимое компонента значения не имеет можно просто возвращать null.

```tsx
// src/Component/docs/props.tsx
import { ILinkProps } from '../Link';

export default function LinkProps(_props: ILinkProps) {
    return null;
}
```

2. В файл code.mdx импортируйте пропсы из файла props.tx через `ts-docgen-loader`

```tsx
// src/Component/docs/props.mdx
import props from "!!ts-docgen-loader!./props.tsx"

<PropsTable props={props}/>

```

## Запуск Storybook

```bash
npm start
```

Storybook доступен по ссылке [http://localhost:8100/](http://localhost:8100/).

## Запуск Dev-сервера с hermione примерами

Текущий Dev-сервер не имеет проводника, чтобы посмотреть собранный пример, перейдите по ссылке: [http://localhost:3000/desktop.react-tests/Link/hermione/hermione.html](http://localhost:3000/desktop.react-tests/Link/hermione/hermione.html)

```bash
BROWSER=0 npm run hermione:dev
```

## Запуск hermione-тестов

1. Cоберите страницу примеров (все примеры собираются в папку `desktop.react-tests`):

  ```bash
  npm run hermione:build
  ```

2. Запустите hermione-тесты.

  Без gui:

  ```bash
  npm run hermione:test
  ```

  С gui:

  ```bash
  npm run hermione:gui
  ```

## Запуск unit-тестов

В качестве фреймворка для тестирования используется <a href='https://github.com/facebook/jest' target='_blank'>jest</a>, для проверки рендера — компонент <a href='https://github.com/airbnb/enzyme' target='_blank'>enzyme</a>.

```bash
# Запуск всех тестов
npm run unit

# Запуск теста по маске (запустит все тесты в папке components/Textinput)
npm run unit Textinput

# Запуск теста в watch-режиме
npm run unit -- --watch Textinput

# Запуск покрытия тестами
npm run unit:coverage
```

В каждом тесте обязательно должны быть проверены все поддерживаемые платформы (`desktop`, `touch-pad`, `touch-phone`), также важно выполнить указанные ниже проверки.

* `server environment :: должен вернуть полный шаблон компонента (snapshot)` — проверяем, что компонент отрендерился на сервере без ошибок (не было обращений к DOM API без проверок).
* `server enviroment :: должен поддерживать миксы через className` — проверяем, что у компонента есть prop className и он прокидывается в DOM-элемент.
* `client environment :: должен вернуть полный шаблон компонента (snapshot)` — проверяем, что компонент отрендерился на клиенте без ошибок.
* `client environment :: должен устанавливать ссылку на корневой DOM-элемент` — проверяем, что компонент поддерживает `innerRef` API для получения ссылки на корневой элемент (если это компонент, который имеет нативный контрол, то должна быть проверка на `controlRef` API).
* `client enviroment :: должен иметь валидный displayName` — проверяем, что у компонента есть свойство `displayName` и он соответствует ему.

## Работа с переводами (i18n)

Для работы с переводами используется библиотека [@yandex-int/i18n](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/i18n). Чтобы Танкер работал с TypeScript, используется специальный парсер и диспатчер из [@yandex-int/tanker-helpers](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-helpers).

```bash
# Выгрузить переводы из tanker
tanker pull

# Загрузить переводы в tanker
tanker push
```

## Cookbook

- Каждый компонент должен реализовывать интерфейс `innerRef` & `controlRef`.

  Свойство `innerRef` должно возвращать ссылку на самый верхний элемент:

  ```tsx
  const textinputRef = createRef()
  const render = () => <Textinput innerRef={textinputRef} />
  // textinputRef.current => <div class="Textinput">...</div>
  ```

  Свойство `controlRef` должно возвращать ссылку на нативный контрол:

  ```tsx
  const textinputRef = createRef()
  const render = () => <Textinput controlRef={textinputRef} />
  // textinputRef.current => <input class="Textinput-Control" />
  ```

- Все свойства интерфейса должны быть описаны в виде JSDoc.

  ```ts
  interface IBlockProps {
    /**
     * Описание свойства.
     * @default 'value'
     */
    property?: string;
  }
  ```

- Использование `defaultProps`.

  Использование с `Stateful component`:

  ```ts
  import { Component, ComponentClass } from 'react'
  import { Defaultize } from '../../typings/utils'
  interface IBlockProps {
    property1?: string
    property2?: string
  }
  const defaultProps = {
    property1: 'value',
  }
  type DefaultProps = keyof typeof defaultProps
  // Создаем тип, в котором свойства, имеющие значения, по умолчанию становятся required,
  // это нужно, чтобы не добавлять проверки на наличие свойства в коде.
  type BlockProps = Defaultize<IBlockProps, DefaultProps>
  export const Block = class extends Component<BlockProps> {
    static defaultProps = defaultProps
    ...
  // Приводим компонент к типу, в котором свойства, имеющие значения, по умолчанию остаются optional.
  } as ComponentClass<IBlockProps>
  ```

  Использование с `functional component`:

  ```ts
  export const Block = ({ property1 = 'value' }) => (
    ...
  )
  ```
