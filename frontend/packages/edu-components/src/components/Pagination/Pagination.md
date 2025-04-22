# Pagination

<!-- description:start -->
Используется для создания пагинации.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { Pagination } from '@yandex-int/edu-components/Pagination/desktop';

const App = () => (
  <Pagination
    currentPage={4}
    totalPages={6}
    renderItem={({ page, title, className, isCurrent }) => (
      <a className={className} {...(!isCurrent && { href: `?page=${page}` })}>
        {title}
      </a>
    )}
  />
);
```

## Свойства

<!-- props:start -->
| Свойство             | Тип                                                  | По умолчанию       | Описание                                        |
| -------------------- | ---------------------------------------------------- | ------------------ | ----------------------------------------------- |
| maxVisibleItemCount? | `number`                                             | `5`                | Максимальное число видимых элементов пагинации. |
| currentPage?         | `number`                                             | `1`                | Текущая страница.                               |
| totalPages           | `number`                                             | —                  | Общее число страниц.                            |
| startItemTitle?      | `string`                                             | `i18n('В начало')` | Название ссылки на первую страницу.             |
| nextItemTitle?       | `string`                                             | `i18n('дальше')`   | Название ссылки на следующую страницу.          |
| renderItem           | `(props: IPaginationItemInjectedProps) => ReactNode` | —                  | Функция отрисовки элемента пагинации.           |
| innerRef?            | `RefObject<HTMLUListElement>`                        | —                  | Ссылка на корневой DOM-элемент компонента.      |
| className?           | `string`                                             | —                  | Дополнительный className.                       |
<!-- props:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Pagination)
