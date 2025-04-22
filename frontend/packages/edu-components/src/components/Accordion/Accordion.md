# Accordion

<!-- description:start -->
Используется для создания раскрывающихся списков.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { Accordion } from '@yandex-int/edu-components/Accordion/desktop';

const App = () => (
  <Accordion
    items={[
      {
        id: 'first',
        content: ({ isOpen, toggle }) => <div>{isOpen ? 'open item' : 'closed item'}</div>,
      },
      {
        id: 'second',
        content: () => 'simple item',
      },
    ]}
  />
);
```

## Свойства

<!-- props:start -->
| Свойство   | Тип                           | Описание                                              |
| ---------- | ----------------------------- | ----------------------------------------------------- |
| items      | `IMixedItem[]`                | Набор элементов.                                      |
| multi?     | `false \| true`               | Разрешить одновременно открывать несколько элементов. |
| innerRef?  | `RefObject<HTMLUListElement>` | Ссылка на корневой DOM-элемент компонента.            |
| className? | `string`                      | Дополнительный className.                             |
<!-- props:end -->

Элементом может быть элемент `ISimpleItem` или группа элементов `IItemGroup`.

### Свойства элемента

| Свойство  | Тип                                                 | Значение по умолчанию | Описание                                                               |
| --------- | --------------------------------------------------- | --------------------- | ---------------------------------------------------------------------- |
| `content` | `(props: IAccordionItemInjectedProps) => ReactNode` | —                     | Отображаемый контент в зависимости от того, открыт элемент или закрыт. |
| `id`      | `string`                                            | —                     | Идентификатор элемента.                                                |

### Свойства группы элементов

| Свойство | Тип             | Значение по умолчанию | Описание                  |
| -------- | --------------- | --------------------- | ------------------------- |
| `id`     | `string`        | —                     | Идентификатор группы.     |
| `items`  | `ISimpleItem[]` | —                     | Набор элементов в группе. |
| `title?` | `ReactNode`     | —                     | Заголовок группы.         |

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Accordion)
