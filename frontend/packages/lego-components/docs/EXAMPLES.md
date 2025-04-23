# Примеры для компонентов

Все примеры написаны для использования в [Storybook][storybook].

## Запуск Storybook

```sh
npm start
```

Storybook доступен по ссылке [http://localhost:8100/](http://localhost:8100/).

## Файловая структура

Все примеры должны распологаться в папке `__examples__`, в данной папке должен быть **только один файл** с экспортом всех примеров `index.examples.ts` и настроек, все остальные файлы не должны содержать постфикс постфикс `examples`.

**Пример файловой структуры:**

```sh
src/Popup/__examples__
├── playground.tsx
├── target.tsx
└── index.examples.ts
```

## Файл конфигурации примеров

Файл `index.examples.ts` должен содержать экспорт всех необходимых примеров, а также [default-export][storybook-meta] содержащий информацию для storybook.

**Пример index.examples.ts:**

```ts
export * from './playground';
export * from './direction';
export * from './target';

export default {
  title: 'Surface/Popup/desktop',
  parameters: {
    docs: {
      readme: require('../readme.md'),
    },
  },
}
```

## Файл примера

Все примеры описываются в новом [storybook-формате][csf], каждый файл должен экспортировать **только один пример** и не содержать локальных зависимостей для корректной работы в [codesandbox][codesandbox].

> **Совет 1:** Используйте во всех примерах бандл компонента. Это помогает лучше находить проблемы и не забывать подключить нужные модификаторы в общую сборку.

> **Совет 2:** Для импорта используйте алиас `@yandex-lego/components` вместо относительного пути - это позволит избежать проблем с открытием примера в [codesandbox][codesandbox].

**Пример target.tsx:**

```tsx
import React from 'react'
import { Popup } from '@yandex-lego/components/Popup/desktop/bundle'

export const Target = () => (
  ...
)
```

[storybook]: https://storybook.js.org
[storybook-meta]: https://storybook.js.org/docs/react/api/csf#default-export
[csf]: https://storybook.js.org/docs/formats/component-story-format/
[codesandbox]: https://codesandbox.io
