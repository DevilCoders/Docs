# Option

<!-- description:start -->
Компонент элемента выбора.
<!-- description:end -->

Может являться частью `MarkerChoice`.

## Примеры

### Пример использования

```ts
import React from 'react';
import { composeU } from '@bem-react/core';
import {
  Option as OptionBase,
  withFlavorMango,
  withFlavorBlueberry,
} from '@yandex-int/edu-components/Option/desktop';

const Option = composeU(withFlavorMango, withFlavorBlueberry)(OptionBase);

const App = () => (
  <Option type="radio" flavor="mango" value="первый" onChange={e => console.log(e.target.value)} />
);
```

### Внешний вид

Чтобы изменить внешний вид маркера, используйте модификатор `_flavor`.

#### blueberry

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-option-blueberry--states%}}

#### mango

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-option-mango--states%}}

#### pumpkin

На сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

{{%story::desktop:edu-components-option-pumpkin--states%}}

#### whiskey

На сервисе должен быть установлен шрифт Suisse или "YS Text", например, с помощью пакета <a href="https://github.yandex-team.ru/lego/islands/tree/dev/packages/yandex-font#yandex-font">yandex-font</a>.

Верные ответы помечаются при проверке зеленым вне зависимости от того, выбрали ли их. Неверные ответы помечаются красным только в том случае, если их выбрали.

{{%story::desktop:edu-components-option-whiskey--states%}}

## Свойства

<!-- props:start -->
| Свойство  | Тип                                                   | По умолчанию | Описание                                                                                                                                                                 |
| --------- | ----------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type      | `"checkbox" \| "radio"`                               | —            | Тип выбора.                                                                                                                                                              |
| value     | `string \| number`                                    | —            | Значение варианта ответа.                                                                                                                                                |
| innerRef? | `RefObject<HTMLLabelElement>`                         | —            | Ссылка на корневой DOM-элемент.                                                                                                                                          |
| name?     | `string`                                              | —            | Название группы, к которой относится вариант.                                                                                                                            |
| checked?  | `false \| true`                                       | —            | Выбранность варианта ответа.                                                                                                                                             |
| disabled? | `false \| true`                                       | `false`      | Отключает интерактивность варианта.                                                                                                                                      |
| readOnly? | `false \| true`                                       | `false`      | Режим просмотра.<br>Вариант не дает изменять значение.                                                                                                                   |
| status?   | `"initial" \| "correct" \| "incorrect" \| "accepted"` | `'initial'`  | Статус варианта ответа. При статусе 'initial' элемент является интерактивным. Остальные статусы являются финальными и убирают возможность взаимодействовать с элементом. |
| onChange? | `(event: ChangeEvent<HTMLInputElement>) => void`      | —            | Коллбэк на выбор варианта ответа.                                                                                                                                        |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид элемента выбора.

**Допустимые значения:** `"blueberry"`, `"coconut"`, `"coconutMilk"`, `"grape"`, `"mango"`, `"pumpkin"`, `"whiskey"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Option)
