# @yandex-market/mbo-form-fields

Этот пакет содержит компоненты полей формы для библиотеки Final Form. Данные компоненты служат для облегчения работы по созданию форм из примитивных элементов, применяя эти компоненты не задумываясь о передачи различной информации в зависимости от типа поля (например обработчика изменения для Select компонента).

Кроме того эти компоненты поддерживают вывод ошибок валидации (красным цветом под полем формы)

## Установка

```bash
npm install @yandex-market/mbo-form-field
```

## Использование

```typescript
import { BaseSelectInput, TextInput, NumberInput, Checkbox, TextArea } from '@yandex-market/mbo-form-field';
```
