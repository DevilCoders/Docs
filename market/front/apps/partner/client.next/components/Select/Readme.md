Компонент для выбора значения из списка.

**HOCS**: [withDropdown](#withdropdown)

```jsx
<div>
    <Select value={select.value} onChange={select.onChange}>
        {select.Options}
    </Select>
</div>
```

Вариант с маленьким количеством опций
```jsx
const options = [
    'Вариант 0',
    'Вариант 1',
    'Вариант 2',
    'Вариант 3',
    'Вариант 4',
    'Вариант 5',
];

<div>
    <Select value={select.value} onChange={select.onChange}>
        {select.Options}
    </Select>
</div>
```

Вертикально - адаптивный
```jsx
const options = [
    'Вариант 0',
    'Вариант 1',
    'Вариант 2',
    'Вариант 3',
    'Вариант 4',
    'Вариант 5',
];

<div>
    <Select value={select.value} onChange={select.onChange} isAdaptive>
        {select.Options}
    </Select>
</div>
```
Группировка опций по лейблу.

```jsx
<div>
    <Select value={select.value} onChange={select.onChange}>
        <OptionList label="label 1">
            {select.Options}
        </OptionList>
        <OptionList label="label 2">
            {select.Options}
        </OptionList>
    </Select>
</div>
```
