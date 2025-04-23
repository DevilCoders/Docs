# Компонент поиска по картинкам

<!-- description:start -->
Компонент поиска по картинкам.
<!-- description:end -->

Компонент ходит за картинками в продакшен картинок по ссылке `//yandex.ru/images/common/`.

## Пример подключения

```tsx
import { Search } from '@yandex-int/images-grid/Search'

const App = () => (
  <Search query="котики" />
)
```

## Параметры запроса

На вкладке `Песочница` представлен стенд, в котором можно указать разные параметры запросов и получить результат в виджете.

## Что внутри

### fetch

Для походов по сети используется https://github.com/lquixada/cross-fetch

### Кастомный скроллбар

Для работы со скроллом используется https://github.com/malte-wessel/react-custom-scrollbars.

Он предусматривает большую вариативность, всё необходимое для работы с ним можно передать в пропс `scrollBarProps`.
Подробнее можно посмотреть в документации скроллбара: https://github.com/malte-wessel/react-custom-scrollbars/tree/master/docs

### ImagesGrid

Внутри компонента находится ImagesGrid, опции для работы с ним можно передать в пропс `imagesGridProps`.

## Обратите внимание

### Когда делать новый запрос?

Чтобы регулировать, в какой момент скролла догружать следующую страницу выдачи передайте свойство `offset` от 0 до 1.
Где 1 это состояние, когда пользователь доскроллил до самого низа.

### Задержка перед запросом

Чтобы регулировать длительностью между запросами (например, чтобы не делать лишние запросы при активном вводе пользователя), передайте опцию `delay`.
Параметр принимает милисекунды, по умолчанию 500.

## Свойства

<!-- props:start -->
| Свойство         | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                                                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| query            | `string`                                                                                                                                                                                                                                                          | —            | Текст запроса.                                                                                                                                     |
| limit?           | `number`                                                                                                                                                                                                                                                          | —            | Количество картинок в ответе.                                                                                                                      |
| iorient?         | `"empty" \| "vertical" \| "horizontal" \| "square"`                                                                                                                                                                                                               | —            | Ориентация изображений.                                                                                                                            |
| isize?           | `"empty" \| "small" \| "large" \| "medium"`                                                                                                                                                                                                                       | —            | Размер изображений.                                                                                                                                |
| type?            | `"empty" \| "photo" \| "clipart" \| "lineart" \| "face" \| "demotivator"`                                                                                                                                                                                         | —            | Тип изображений.                                                                                                                                   |
| family?          | `0 \| 1 \| 2`                                                                                                                                                                                                                                                     | —            | Фильтрация контента, по умолчанию, семейный поиск. 1 – семейный поиск. 2 – умеренный поиск. 0 – без фильтрации.                                    |
| addonAfter?      | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Дополнительный контент после сетки                                                                                                                 |
| addonBefore?     | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Дополнительный контент перед сеткой                                                                                                                |
| onClick?         | `(event: MouseEvent<HTMLElement, MouseEvent>, payload: DocProps) => void`                                                                                                                                                                                         | —            | Обработчик клика на картинку.                                                                                                                      |
| delay?           | `number`                                                                                                                                                                                                                                                          | —            | Задержка между запросами, ms.                                                                                                                      |
| imagesGridProps? | `{ addonAfter?: ReactNode; addonBefore?: ReactNode; innerRef?: RefObject<HTMLDivElement>; className?: string; imageClassName?: string; ... 7 more ...; baseRowHeight?: number; }`                                                                                 | —            | Свойства для ImagesGrid.                                                                                                                           |
| scrollBarProps?  | `{ onClick?: (event: MouseEvent<Scrollbars, MouseEvent>) => void; className?: string; cols?: number; width?: ReactText; onScroll?: (event: UIEvent<any>) => void; ... 373 more ...; key?: ReactText; }`                                                           | —            | Свойства для Scrollbars 'react-custom-scrollbars'.                                                                                                 |
| offset?          | `number`                                                                                                                                                                                                                                                          | `0.8`        | В какой момент скролла догружать следующую страницу выдачи? Значение от 0 до 1. Где 1 это состояние, когда пользователь доскроллил до самого низа. |
<!-- props:end -->
