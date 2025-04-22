# Spoiler

<!-- description:start -->
Компонент для отображения скрытого содержимого.
<!-- description:end -->

## Примеры

### Пример использования

```tsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
  Spoiler as SpoilerBase,
  withSticky,
  withFlavorGrape,
} from '@yandex-int/edu-components/Spoiler/desktop';

// Соберите компонент с нужными свойствами
const Spoiler = compose(
  withSticky,
  withFlavorGrape,
)(SpoilerBase);

// Используйте в приложении
const App = () => (
  <Spoiler
    sticky
    flavor="grape"
    caption="Страшный спойлер"
    onToggle={open => console.log(open ? 'открыт' : 'закрыт')}
  >
    Лору Палмер убил её отец
  </Spoiler>
);
```

### Внешний вид

Чтобы изменить внешний вид спойлера, используйте модификатор `_flavor`.

#### grape

{{%story::desktop:edu-components-spoiler-grape-desktop--default%}}

## Свойства

<!-- props:start -->
| Свойство   | Тип                                                                                                                                                                                                                                                               | По умолчанию      | Описание                                                                                               |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------ |
| children?  | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —                 | Содержимое спойлера.                                                                                   |
| caption?   | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | `i18n('Спойлер')` | Подпись к спойлеру, по клику на которую происходит открытие/закрытие.                                  |
| open?      | `false \| true`                                                                                                                                                                                                                                                   | `false`           | Указывает, будет ли содержимое спойлера изначально отображено или скрыто.                              |
| onToggle?  | `(open: boolean) => void`                                                                                                                                                                                                                                         | —                 | Обработчик, срабатывающий на открытие/закрытие спойлера и передающий его состояние.                    |
| innerRef?  | `(instance: HTMLDetailsElement) => void \| RefObject<HTMLDetailsElement>`                                                                                                                                                                                         | —                 | Ссылка на корневой DOM-элемент компонента.                                                             |
| className? | `string`                                                                                                                                                                                                                                                          | —                 | Дополнительный className.                                                                              |
| testName?  | `string`                                                                                                                                                                                                                                                          | —                 | Имя теста. На его основе генерируются атрибуты data-test-name для элементов спойлера. См. Тестирование |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид спойлера.

**Допустимые значения:** `"grape"`.

### sticky

Включает залипание подписи открытого спойлера.
Работает только в браузерах с поддержкой `position: sticky`.

**Допустимые значения:** `false`, `true`.

{{%story::desktop:edu-components-spoiler-grape-desktop--sticky%}}
<!-- modifiers:end -->

## Тестирование

Если передать свойство `testName`, на маркер и варианты выбора будут выставлены атрибуты `data-test-name`.
Рекомендуется передавать это свойство либо при `NODE_ENV=testing`, либо воспользоваться [babel-plugin-react-remove-properties](https://www.npmjs.com/package/babel-plugin-react-remove-properties).

```ts
import { testNames, convertToSelectors, Spoiler } from '@yandex-int/edu-components/Spoiler/desktop';

const testName = 'myTest';

// Передайте testName в тестируемый компонент
<Spoiler
    ...
    testName={testName}
/>

// Получите селекторы для доступа к элементам
const selectors = convertToSelectors(testNames(testName));

// Используйте их в тестах
const spoilerSelector = selectors.spoiler;
const triggerSelector = selectors.trigger;
const contentSelector = selectors.content;
```

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Spoiler)
