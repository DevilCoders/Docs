# Sideblock

<!-- description:start -->
Используется для создания модального окна, которое выезжает из-за границы окна браузера.
<!-- description:end -->

## Пример использования

```ts
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import { withOutsideClick } from '@yandex-lego/components/withOutsideClick';
import { Sideblock as SideblockBase, withThemeNormal } from '@yandex-int/edu-components/Sideblock/desktop';

const Sideblock = compose(
  withOutsideClick,
  withThemeNormal,
)(SideblockBase);

const App = () => {
  const [visible, setVisible] = useState(false);

  return (
    <Sideblock
      hasBlockingBackground
      theme="normal"
      visible={visible}
      onOutsideClick={() => setVisible(false)}
      onEscapeKeyDown={() => setVisible(false)}
      style={{ width: 500 }}
    >
      <div>content</div>
    </Sideblock>
  );
};
```

## Свойства

Компонент является частным случаем `Popup` и расширяет интерфейс `IPopupProps`.

<!-- props:start -->
| Свойство                 | Тип                                                                                                                                                                                                                                                               | По умолчанию    | Описание                                                                                                                                                                                                                                                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| side?                    | `"top" \| "right" \| "bottom" \| "left"`                                                                                                                                                                                                                          | `'right'`       | Расположение сайдблока относительно окна браузера.                                                                                                                                                                                                                                                                   |
| hasAnimation?            | `false \| true`                                                                                                                                                                                                                                                   | `true`          | Наличие анимации при открытии.<br>Анимация есть только на уровне `desktop`.                                                                                                                                                                                                                                          |
| hasBlockingBackground?   | `false \| true`                                                                                                                                                                                                                                                   | `false`         | Наличие блокирующей затемняющей подложки.<br>Без блокировки страницы прокручиваются и сайдблок, и страница.<br> При блокировке страницы прокручиваются только контент сайдблока.                                                                                                                                     |
| addonAfter?              | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —               | Дополнительный контент после содержимого попапа                                                                                                                                                                                                                                                                      |
| addonBefore?             | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —               | Дополнительный контент перед содержимым попапа                                                                                                                                                                                                                                                                       |
| direction?               | `"bottom-left" \| "bottom-center" \| "bottom-right" \| "top-left" \| "top-center" \| "top-right" \| "right-top" \| "right-center" \| "right-bottom" \| "left-top" \| "left-center" \| "left-bottom"`                                                              | —               | Задает направление хвостика. Например, если указано значение `bottom-center` — хвостик выходит из центра снизу.<br>Свойство `direction` необходимо использовать без модификатора `_target_anchor`. Чтобы задать направление раскрытия для попапа с модификатором `_target_anchor`, используйте свойство `directions` |
| forceRender?             | `false \| true`                                                                                                                                                                                                                                                   | —               | Вызывает дополнительный рендер после создания                                                                                                                                                                                                                                                                        |
| hasTail?                 | `false \| true`                                                                                                                                                                                                                                                   | —               | Включает/отключает хвостик у попапа                                                                                                                                                                                                                                                                                  |
| innerRef?                | `RefObject<HTMLDivElement>`                                                                                                                                                                                                                                       | —               | Ссылка на корневой DOM-элемент компонента                                                                                                                                                                                                                                                                            |
| keepMounted?             | `false \| true`                                                                                                                                                                                                                                                   | `true`          | Сохраняет контейнер в DOM после создания                                                                                                                                                                                                                                                                             |
| position?                | `{ top?: number; left?: number; bottom?: number; right?: number; }`                                                                                                                                                                                               | —               | Задает позицию попапа. Свойство `position` необходимо использовать без модификатора `_target_anchor`                                                                                                                                                                                                                 |
| scope?                   | `RefObject<HTMLElement>`                                                                                                                                                                                                                                          | `document.body` | Ссылка на DOM-элемент, в котором размещается попап<br>Важно, чтобы контейнер имел `position: relative` для корректного позициоинирования.                                                                                                                                                                            |
| tailPosition?            | `{ top: number; left: number; }`                                                                                                                                                                                                                                  | —               | Задает позицию хвостика. Свойство `tailPosition` необходимо использовать без модификатора `_target_anchor`.                                                                                                                                                                                                          |
| tailRef?                 | `RefObject<HTMLDivElement>`                                                                                                                                                                                                                                       | —               | Ссылка на DOM-элемент хвостика                                                                                                                                                                                                                                                                                       |
| tailSize?                | `number`                                                                                                                                                                                                                                                          | —               | Задает размер хвостика                                                                                                                                                                                                                                                                                               |
| targetRef?               | `RefObject<HTMLElement>`                                                                                                                                                                                                                                          | —               | Ссылка на DOM-элемент, в котором не отслеживаются нажатия. Используется с `withOutsideClick`                                                                                                                                                                                                                         |
| visible?                 | `false \| true`                                                                                                                                                                                                                                                   | —               | Делает попап видимым                                                                                                                                                                                                                                                                                                 |
| zIndex?                  | `number`                                                                                                                                                                                                                                                          | —               | Задает слой `z-index`                                                                                                                                                                                                                                                                                                |
| className?               | `string`                                                                                                                                                                                                                                                          | —               | Дополнительный класс                                                                                                                                                                                                                                                                                                 |
| style?                   | `CSSProperties`                                                                                                                                                                                                                                                   | —               | Html атрибут `style`                                                                                                                                                                                                                                                                                                 |
| unstable_onRenderTail?   | `(tail: ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)>) => ReactElement<...>`                                                | —               | Функция, вызывающаяся при отрисовке хвостика. Вызывается вне зависимости от наличия флага `hasTail`.                                                                                                                                                                                                                 |
| unstable_setTailContent? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —               | Функция, проставляющая контент для хвостика                                                                                                                                                                                                                                                                          |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### theme

Задает стилевое оформление сайдблока.

**Допустимые значения:** `"normal"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Sideblock)
