# StatusBadge

<!-- description:start -->
Компонент для отображения значка статуса ответа маркера.
<!-- description:end -->

## Свойства
<!-- props:start -->
| Свойство   | Тип                                                                                                                                                                                                                                                                                                                  | Описание                                            |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| status     | `"correct" \| "incorrect" \| "skipped"`                                                                                                                                                                                                                                                                              | Статус.                                             |
| innerRef?  | `RefObject<HTMLDivElement>`                                                                                                                                                                                                                                                                                          | Ссылка на корневой DOM-элемент компонента.          |
| className? | `string`                                                                                                                                                                                                                                                                                                             | Дополнительный className.                           |
| children?  | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal \| (props: IStatusBadgeInjectedProps) => ReactNode` | Элемент, который вставляется в тело значка статуса. |
| style?     | `CSSProperties`                                                                                                                                                                                                                                                                                                      | Стили значка статуса.                               |
<!-- props:end -->

## Модификаторы
<!-- modifiers:start -->
### hasImage

Задает значку статуса изображение.

| Свойство            | Тип                                                  | Описание                                                                                           |
| ------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| hasImage?           | `false \| true`                                      | Наличие изображения у значка статуса.                                                              |
| getImageSource?     | `(status: TBadgeStatus, density?: number) => string` | Функция для загрузки локальных изображений. Используется для построение атрибута `srcset`.         |
| availableDensities? | `number[]`                                           | Плотности пикселей экранов для которых подготовлены изображения. Используется в атрибуте `srcset`. |
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/StatusBadge)
