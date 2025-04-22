# MarkerChoice

<!-- description:start -->
Компонент для view задачи на выбор текста, картинок, формул из списка.
Задается условие задачи, элементы выбора. Нужно выбрать один или несколько элементов.
Single choice and multiple choice.
<!-- description:end -->

Может использоваться вместе с `Option`.

## Примеры

### Пример использования

```ts
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import { withRegistry, Registry } from '@bem-react/di';
import {
  cnMarkerChoice,
  MarkerChoice as MarkerChoiceBase,
  withTypeCheckbox,
  withTypeRadio,
  withLayoutHorizontal,
  withFlavorMango,
} from '@yandex-int/edu-components/MarkerChoice/desktop';
import {
  Option as OptionBase,
  withFlavorMango as withOptionFlavorMango,
} from '@yandex-int/edu-components/Option/desktop';

// Собираем компонент элемента выбора
const Option = withOptionFlavorMango(OptionBase);

// Создаем реестр
const markerChoiceRegistry = new Registry({ id: cnMarkerChoice() });

// Устанавливаем в него собранный элемент
markerChoiceRegistry.set('Option', Option);

// Собираем маркер
const MarkerChoice = compose(
  withRegistry(markerChoiceRegistry),
  composeU(withTypeCheckbox, withTypeRadio),
  withLayoutHorizontal,
  withFlavorMango,
)(MarkerChoiceBase);

// Используем в приложении
const App = () => (
  <MarkerChoice
    type="radio"
    flavor="mango"
    layout="horizontal"
    options={['первый', 'второй', 'третий']}
    value={[]}
    onChange={e => console.log(e.target.value)}
  />
);
```

### Внешний вид

Чтобы изменить внешний вид маркера, используйте модификатор `_flavor`.

#### blueberry

{{%story::desktop:edu-components-markerchoice-blueberry--states%}}

#### mango

{{%story::desktop:edu-components-markerchoice-mango--states%}}

#### pumpkin

{{%story::desktop:edu-components-markerchoice-pumpkin--states%}}

#### whiskey

{{%story::desktop:edu-components-markerchoice-whiskey--states%}}

### Раскладка

Чтобы изменить расположение элементов в маркере, используйте модификатор `_layout`.

{{%story::desktop:edu-components-markerchoice-blueberry--layouts%}}

## Свойства

<!-- props:start -->
| Свойство        | Тип                                              | По умолчанию | Описание                                                                                                                  |
| --------------- | ------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------- |
| type            | `"checkbox" \| "radio"`                          | —            | Тип выбора.                                                                                                               |
| value           | `number[]`                                       | —            | Текущее значение.                                                                                                         |
| className?      | `string`                                         | —            | Дополнительный класс.                                                                                                     |
| innerRef?       | `RefObject<HTMLUListElement>`                    | —            | Ссылка на корневой DOM-элемент.                                                                                           |
| name?           | `string`                                         | `choice`     | Название группы вариантов маркера. Передается в Option.                                                                   |
| options?        | `ReactNode[]`                                    | `[]`         | Массив вариантов ответа.                                                                                                  |
| disabled?       | `false \| true`                                  | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                   |
| readOnly?       | `false \| true`                                  | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно.   |
| statuses?       | `TAnswerStatus[]`                                | `[]`         | Статусы вариантов ответов.                                                                                                |
| testName?       | `string`                                         | —            | Имя теста. На его основе генерируются атрибуты data-test-name для элементов маркера. См. Тестирование                     |
| flavor?         | `string`                                         | —            | Внешний вид. Передается в Option.                                                                                         |
| onChoiceChange? | `(event: ChangeEvent<HTMLInputElement>) => void` | —            | Коллбэк на изменение одного из вариантов ответов. Не используется с модификаторами \_type. Возвращает измененный элемент. |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид маркера.

**Допустимые значения:** `"blueberry"`, `"mango"`, `"pumpkin"`, `"whiskey"`.

### type

Задает тип выбора, множественный или единственный.

В ответ на изменение ответа пользователя отправляет весь измененный ответ целиком.

| Свойство  | Тип                                              | Описание                                  |
| --------- | ------------------------------------------------ | ----------------------------------------- |
| type?     | `"checkbox" \| "radio"`                          | Тип выбора.                               |
| onChange? | `(e: { target: { value: number[]; }; }) => void` | Коллбэк на изменения ответа пользователя. |

### layout

Задает расположение вариантов ответа.

**Допустимые значения:** `"2cols"`, `"3cols"`, `"horizontal"`, `"vertical"`.
<!-- modifiers:end -->

## Тестирование

Если передать свойство `testName`, на маркер и варианты выбора будут выставлены атрибуты `data-test-name`.
Рекомендуется передавать это свойство только при `NODE_ENV=testing`:

```ts
import { testNames, convertToSelectors, MarkerChoice } from '@yandex-int/edu-components/MarkerChoice/desktop';

const testName = 'myTest';

// Передайте testName в тестируемый компонент
<MarkerChoice
    ...
    testName={testName}
/>

// Получите селекторы для доступа к элементам
const selectors = convertToSelectors(testNames(testName));

// Используйте их в тестах
const markerSelector = selectors.marker;
const optionSelector = selectors.option;
const checkedOptionSelector = selectors.checkedOption;
```

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerChoice)
- [Описание формата](https://docs.pelican.common.yandex.ru/formats/markers/choice.html)
