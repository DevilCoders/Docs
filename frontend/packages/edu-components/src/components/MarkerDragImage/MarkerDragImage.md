# MarkerDragImage

<!-- description:start -->
Компонент для view задачи с механикой перетаскивания картинок.
<!-- description:end -->

**Важно**: Компонент использует [react-dnd](https://github.com/react-dnd/react-dnd/) и `react-dnd-html5-backend`

## Свойства
<!-- props:start -->
| Свойство         | Тип                                        | Описание                                     |
| ---------------- | ------------------------------------------ | -------------------------------------------- |
| className?       | `string`                                   | Дополнительный класс.                        |
| readOnly?        | `false \| true`                            | Флаг ридонли.                                |
| innerRef?        | `RefObject<HTMLDivElement>`                | Ссылка на корневой элемент компоненнта       |
| onChange?        | `() => void`                               | Обработчик изменения ответа.                 |
| value?           | `unknown`                                  | Ответ пользователя.                          |
| backgroundMarkup | `{ width: number; x: number; y: number; }` | Разметка фоновой картинки механики.          |
| backgroundSrc    | `string`                                   | Ссылка на фоновую картинку.                  |
| choicesSrc       | `string[]`                                 | Ссылки на картинки для вариантов ответа.     |
| choicesMarkup    | `TChoiceMarkup[]`                          | Разметка вариантов ответа.                   |
| markerWidth?     | `number`                                   | Ширина корневого компонента механики.        |
| fieldsMarkup     | `TFieldMarkup[]`                           | Разметка "полей ввода" для вариантов ответа. |
| multipleChoices? | `false \| true`                            | Флаг возможности множественного выбора.      |
<!-- props:end -->


## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerDragImage)
- [Описание формата](https://docs.schoolbook.education.yandex-team.ru/formats/markers/dragimage.html)
