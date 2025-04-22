# Модификация компонента

Если дизайн `@yandex-lego/components` не подходит для вашего проекта, вы можете:

1. Изменить [тему](https://lego.yandex-team.ru/components/lego/latest/?storybook=%2Fdocs%2Futility-theme--docs) для проекта.
2. Написать визуальный [модификатор](#кастомизация-модификатора) для компонента.

Все компоненты можно использовать без поставляемых в пакете модификаторов и тем, реализуя свои и не увеличивая размер итогового бандла.

## Кастомизация модификатора

На данный момент визуал почти каждого компонента состоит из двух модификаторов:

- `size` — содержит размеры самого компонента и его типографики;
- `view` — содержит визуальное оформление компонента и различные его состояния (например, hovered, focused, disabled).

> **Примечание.** Если нет необходимости в разных размерах, весь визуал можно реализовать в рамках модификатора `view`.

### Реализация собственного модификатора

Создадим новый визуальный модификатор `view` со значением `custom` для компонента `Button`.

![image](https://media.github.yandex-team.ru/user/5546/files/f0435000-567f-11ea-89fb-6cfce6b08547)

1. Создадим CSS-файл и напишем там немного стилей (за основу можно взять уже существующий модификатор):

  ```css
  /* src/Button/_view/Button_view_custom.css */
  .Button2_view_custom {
    color: #fff;
    height: 36px;
    font-size: 15px;
    line-height: 36px;
  }

  .Button2_view_custom::before {
    background-color: #000;
  }

  .Button2_view_custom:active {
    background-color: #222;
  }

  .Button2_view_custom:not([aria-disabled='true']):hover::before {
    background-color: #444;
  }
  ```

2. Создадим `tsx`-файл и опишем логику подключения:

  ```ts
  /* src/Button/_view/Button_view_custom.tsx */
  import { withBemMod } from '@bem-react/core'
  import { cnButton } from '@yandex-lego/components/Button'

  import './Button_view_custom.css'

  export interface IButtonViewCustomProps {
    view?: 'custom'
  }

  export const withViewCustom = withBemMod<IButtonViewCustomProps>(cnButton(), {
    view: 'custom',
  })
  ```

[structure]: https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/Theme/Theme.md#тема
[preset]: https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/Theme/Theme.md#пресет
[root-theme-apply]: https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/Theme/Theme.md#на-клиенте
[feature-theme-apply]: https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/Theme/Theme.md#в-рамках-фичи
