# MarkerInline

<!-- description:start -->
Компонент для view задачи, в тексте которой есть поля ввода.
<!-- description:end -->

## Примеры

### Пример использования

```typescript jsx
import React, { FC } from 'react';
import { compose } from '@bem-react/core';
import { withRegistry, Registry } from '@bem-react/di';
import {
  cnMarkerInline,
  MarkerInline as MarkerInlineBase,
  withRuleInput,
} from '@yandex-int/edu-components/MarkerInline/desktop';
import {
  Markdown as MarkdownBase,
  withRuleBrSign,
  withRuleSub,
  withRuleSup,
} from '@yandex-int/edu-components/Markdown/desktop';

// Создаем реестр
const markerInlineRegistry = new Registry({ id: cnMarkerInline() });

// Собираем компонент Markdown с нужными правилами
const Markdown = compose(
  withRuleInput, // правило обработки инпутов из MarkerInline
  withRuleBrSign,
  withRuleSub,
  withRuleSup,
)(MarkdownBase);

// Импортируем компонент InlineInput с нужными типами (см. пример реализации далее).
import { InlineInput } from './InlineInput';

// Устанавливаем собранные элементы в реестр MarkerInline
markerInlineRegistry.set('Input', InlineInput);
markerInlineRegistry.set('Markdown', Markdown);

// Собираем маркер
const MarkerInline = withRegistry(markerInlineRegistry)(MarkerInlineBase);

// Используем в приложении
const App = () => (
  <MarkerInline
    inputs={{
      '3': {
        type: 'comma',
        group: 1,
        options: {
          type_display: 'visible',
        },
      },
      '4': {
        type: 'separator',
        group: 2,
        options: {
          choices: ['hyphen', 'together'],
        },
      },
    }}
    value={{ '3': true, '4': 0 }}
    status={{ '3': 'incorrect', '4': 'correct' }}
    onChange={e => console.log(e.target.value)}
  >
    {'Какой{input:4}то текст с{input:3} разными инпутами'}
  </MarkerInline>
);
```

### Пример компонента InlineInput

Компонент должен реализовывать интерфейс `IMarkerInlineInputProps`:

```typescript jsx
interface IMarkerInlineInputProps {
  id: string;
  type: string;
  group: number;
  options?: object;
  value?: any;
  status: 'correct' | 'incorrect' | 'initial';
  readOnly: boolean;
  disabled: boolean;
  onChange: (value: any) => void;
}
```

Компонент должен мапить тип инпута из тех, что используются на сервисе, в конкретную реализацию, например, так:

[Подробный пример реализации](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerInline/MarkerInline.examples/InlineInput)

```typescript jsx
export const InlineInput: FC<IMarkerInlineInputProps> = ({ type }) => {
  switch (type) {
    case 'field':
      return <Field />;
    case 'sequence':
      return <MarkerSequence />;
    case 'separator':
      return <MarkerSeparator />;
    default:
      return null;
  }
};
```

В библиотеке реализованы:

| type      | Основа компонента | Примечание                                                         |
| --------- | ----------------- | ------------------------------------------------------------------ |
| field     | `Field`           |                                                                    |
| choice    | —                 | Пока можно воспользоваться Select из Лего или своей реализацией    |
| comma     | `MarkerSeparator` |                                                                    |
| separator | `MarkerSeparator` |                                                                    |
| rational  | —                 | Пока можно воспользоваться Textinput из Лего или своей реализацией |
| sequence  | `MarkerSequence`  |                                                                    |

## Свойства

<!-- props:start -->
| Свойство         | Тип                                                  | По умолчанию | Описание                                                                                                                                                     |
| ---------------- | ---------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| children         | `string`                                             | —            | Строка, в которую вписаны инпуты в формате `{input:id}`                                                                                                      |
| value?           | `{ [x: string]: Record<string, unknown>; }`          | `{}`         | Структура, содержащая значения инпутов. Объект, где ключи — идентификаторы инпутов, а значения — соответствующие значения.                                   |
| status?          | `{ [x: string]: Record<string, unknown>; }`          | `{}`         | Структура, содержащая статусы инпутов. Объект, где ключи — идентификаторы инпутов, а значения — соответствующие статусы.                                     |
| onChange?        | `(e: { target: { value: unknown; }; }) => void`      | —            | Обработчик, срабатывающий на изменение инпута и передающий новое значение маркера.                                                                           |
| readOnly?        | `false \| true`                                      | `false`      | Режим просмотра. Передаётся в input.                                                                                                                         |
| disabled?        | `false \| true`                                      | `false`      | Неактивный режим. Передаётся в input.                                                                                                                        |
| className?       | `string`                                             | —            | Дополнительный класс.                                                                                                                                        |
| innerRef?        | `RefObject<HTMLDivElement>`                          | —            | Ссылка на корневой DOM-элемент.                                                                                                                              |
| additionalState? | `{ [x: string]: unknown; }`                          | —            | Внутренний компонент Markdown можно расширять правилами, которые требуют дополнительны полей в стейте. Этот проп позволяет прокинуть эти дополнительные поля |
| modes            | `IMode<IModeOptions>[]`                              | —            | Список режимов с их описанием                                                                                                                                |
| activeMode?      | `"inline" \| "syntax" \| "separator" \| "paragraph"` | —            | Активный режим (может быть только один)                                                                                                                      |
<!-- props:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerInline)
- [Описание формата](https://docs.pelican.common.yandex.ru/formats/markers/inline.html)
