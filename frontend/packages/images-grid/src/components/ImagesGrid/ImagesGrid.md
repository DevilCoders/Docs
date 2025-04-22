# Сетка изображений

<!-- description:start -->
Компонент сетки из изображений.
<!-- description:end -->

Для вычисления выравнивания используется компонент из Турбо: https://github.yandex-team.ru/serp/turbo/tree/dev/platform/components/MMJustifier
## Пример подключения

```tsx
import { ImagesGrid } from '@yandex-int/images-grid/ImagesGrid/desktop/bundle'

const App = () => (
  <ImagesGrid images=[...]/>
)

```

## Примеры

### Распределение картинок по колонкам

У сетки бывает два вида: выравнивание по рядам и по колонкам. (За это отвечает свойство layout).
Чтобы картинки равномерно располагались по указаному числу колонок, надо выставить `layout="vertical"` и передать нужное количество столбцов: `cols={2}`

{{%story::yandex-int-imagesgrid-imagesgrid-desktop--vertical%}}

### Распределение картинок по строчкам

Чтобы картинки равномерно располагались по ширине (количество в ряду подбиралось программно), то нужно передать `layout="horizontal"`

{{%story::yandex-int-imagesgrid-imagesgrid-desktop--horizontal%}}

### Ошибка

Для того, чтобы показать сообщение об ошибке, передайте в компонент непустой обработчик `onRetryLoad`.
Он будет вызываться по клику на кнопку в сообщении об ошибке.

{{%story::yandex-int-imagesgrid-imagesgrid-desktop--error%}}


## Свойства
<!-- props:start -->
| Свойство        | Тип                                                                                                                                                                                                                                                               | Описание                                     |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| innerRef?       | `(instance: HTMLElement) => void \| RefObject<HTMLElement>`                                                                                                                                                                                                       | Ссылка на корневой DOM элемент компонента.   |
| className?      | `string`                                                                                                                                                                                                                                                          | Дополнительный класс контейнера.             |
| imageClassName? | `string`                                                                                                                                                                                                                                                          | Дополнительный класс для изображений.        |
| onClick?        | `(event: MouseEvent<HTMLElement, MouseEvent>, payload: ImageProps) => void`                                                                                                                                                                                       | Обработчик клика на картинку.                |
| layout?         | `"vertical" \| "horizontal"`                                                                                                                                                                                                                                      | Горизонтальная или вертикальная выдача.      |
| images?         | `ImageProps[]`                                                                                                                                                                                                                                                    | Список картинок.                             |
| cols?           | `number`                                                                                                                                                                                                                                                          | Количество колонок                           |
| width?          | `number`                                                                                                                                                                                                                                                          | Ширина контейнера                            |
| minImageWidth?  | `number`                                                                                                                                                                                                                                                          | Минимальная ширина изображения               |
| gap?            | `number`                                                                                                                                                                                                                                                          | Отступы между ячейками                       |
| rowMarginRight? | `number`                                                                                                                                                                                                                                                          | Отступы между ячейками для вычисления сетки. |
| baseRowHeight?  | `number`                                                                                                                                                                                                                                                          | Базовая высота строки для вычисления сетки.  |
| onRetryLoad?    | `() => void`                                                                                                                                                                                                                                                      | Показать сообщение об ошибке                 |
| addonAfter?     | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент после сетки           |
| addonBefore?    | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент перед сеткой          |
| cut?    | `boolean` | Прятать изображения, которые не попадают в колоночную сетку.          |
<!-- props:end -->
