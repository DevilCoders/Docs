# BottomFooter

Необходим для отображения внизу страницы какого-то фиксированного блока. Обычно это кнопки действия над выделенным
объектом или кнопки отправки формы.

## Props

| Свойство   | Тип         | Умолчание | Описание                     |
| ---------- | ----------- | --------- | ---------------------------- |
| `cls?`     | `string`    | `''`      | Класс CSS                    |
| `children` | `ReactNode` | -         | Произвольное тело компонента |

## Пример

```typescript
import { BottomFooter } from '@yandex-infracloud-ui/libs';

function Example() {
   return (
      <BottomFooter>
         <h1>Any child</h1>
      </BottomFooter>
   );
}
```
