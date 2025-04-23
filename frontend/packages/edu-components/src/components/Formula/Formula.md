# Formula

<!-- description:start -->
Компонент для рендера формул в формате [LaTeX](https://www.latex-project.org/).
<!-- description:end -->

## Пример использования

```typescript jsx
import React from 'react';
import { Formula } from '@yandex-int/edu-components/Formula/desktop';

const App = () => <Formula code="\\binom{n}{k}" multiline />;
```

## Свойства

<!-- props:start -->
| Свойство     | Тип                                                                 | По умолчанию | Описание                                                    |
| ------------ | ------------------------------------------------------------------- | ------------ | ----------------------------------------------------------- |
| code?        | `string`                                                            | `''`         | Разметка в формате [LaTeX](https://www.latex-project.org/). |
| multiline?   | `false \| true`                                                     | —            | Флаг многострочности формулы.                               |
| className?   | `string`                                                            | —            | Дополнительный класс.                                       |
| innerRef?    | `(instance: TFormulaElement) => void \| RefObject<TFormulaElement>` | —            | Ссылка на корневой DOM-элемент компонента.                  |
| onReady?     | `() => void`                                                        | —            | Коллбэк на рендер формулы.                                  |
| preProcess?  | `(code: string) => string`                                          | —            | Функция для подготовки разметки к трансформации в HTML.     |
| postProcess? | `(html: string) => string`                                          | —            | Функция для обработки HTML после трансформации.             |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### hasInputs

Задает рендер инпутов в формуле.

| Свойство         | Тип                                          | По умолчанию               | Описание                                                                                                                                       |
| ---------------- | -------------------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| hasInputs?       | `false \| true`                              | —                          | Флаг наличия инпутов.                                                                                                                          |
| inputRegex?      | `RegExp`                                     | `DEFAULT_INPUT_REGEX`      | Регулярное выражение для поиска разметки инпутов.                                                                                              |
| placeholderStub? | `string`                                     | `DEFAULT_PLACEHOLDER_STUB` | Строка, которой точно нет в разметке формулы.                                                                                                  |
| readOnly         | `false \| true`                              | —                          | Режим просмотра. Передаётся в input.                                                                                                           |
| disabled         | `false \| true`                              | —                          | Неактивный режим. Передаётся в input.                                                                                                          |
| inputs           | `{ [x: string]: TInlineInputData; }`         | —                          | Структура, содержащая описания инпутов (type, group, options). Объект, где ключи — идентификаторы инпутов, а значения — объект с их описанием. |
| status           | `{ [x: string]: TAnswerStatus; }`            | —                          | Структура, содержащая статусы инпутов. Объект, где ключи — идентификаторы инпутов, а значения — соответствующие статусы.                       |
| value            | `{ [x: string]: any; }`                      | —                          | Структура, содержащая значения инпутов. Объект, где ключи — идентификаторы инпутов, а значения — соответствующие значения.                     |
| onChange         | `(inputId: string, inputValue: any) => void` | —                          | Обработчик, срабатывающий на изменение инпута.                                                                                                 |
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Formula)
