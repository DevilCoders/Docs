Дропдаун для тача с нативным отображением элементов

Примеры:

```jsx
const optionsList = [
    {
        text: 'Это',
        value: 'Это',
    },
    {
        text: 'Вон то',
        value: 'Вон то',
    },
    {
        text: 'То',
        value: 'То',
    },
];

<DropdownNative options={optionsList} value='Вон то' />
```

С заданной шириной:

```jsx
const optionsList = [
    {
        text: 'Йа с заданной шыриной',
        value: 'Йа с заданной шыриной',
    },
];

<DropdownNative options={optionsList} width='300' />
```

Во всю ширину:

```jsx
const optionsList = [
    {
        text: 'Йа шырокий',
        value: 'Йа шырокий',
    },
];

<DropdownNative options={optionsList} width='auto' />
```
