# Hint

Отображает подсказку при клике на иконку. Подсказка может быть текстовой или сложной (содержащей JSX).

## Props

| Свойство | Тип         | Умолчание | Описание                                   |
| :------- | :---------- | :-------- | :----------------------------------------- |
| `cls?`   | `string`    | `''`      | Класс CSS                                  |
| `text?`  | `ReactNode` | `''`      | Текстовое содержимое для простых подсказок |

## Пример

```typescript jsx
import { Hint } from '@yandex-infracloud-ui/libs';

function Example() {
   return <Hint text='Текст подсказки' />;
}
```

<!-- STORY -->
