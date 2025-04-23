Компонент для выбора значения из списка.

**HOCS**: [withDropdown](#withdropdown)

```jsx
const select = ctx.Select({state, setState});

const {initialState, onChange} = select;

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

const select = ctx.Select({options, state, setState});

const {initialState, onChange, Options} = select;

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

const select = ctx.Select({options, state, setState});

const {initialState, onChange, Options} = select;

<div>
    <Select value={select.value} onChange={select.onChange} isAdaptive>
        {select.Options}
    </Select>
</div>
```
Группировка опций по лейблу.

```jsx
const OptionList = require('./OptionList').default;

const select = ctx.Select({state, setState});

const {initialState, onChange} = select;

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
