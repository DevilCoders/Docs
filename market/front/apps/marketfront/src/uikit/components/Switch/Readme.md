## Свитчер

### Песочница
```js noeditor
<Helper.Playground
    component={Switch}
    defaultValues={{children: 'беру!'}}
/>
```

### Примеры
### `checked`

#### `checked={false}` (default)
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Выключенный переключатель"
    checked={checked}
    onChange={onChange}
/>
```

#### `checked={true}`
```jsx
const [checked, setChecked] = React.useState(true);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Включенный переключатель"
    checked={checked}
    onChange={onChange}
/>
```

### `disabled`
#### `disable={false}` (default)

#### Неактивный выключен
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Неактивный переключатель"
    disabled={true}
    checked={checked}
    onChange={onChange}
/>
```

#### `disable={true}`
```jsx
const [checked, setChecked] = React.useState(true);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Неактивный переключатель"
    disabled={true}
    checked={checked}
    onChange={onChange}
/>
```

### `size`

#### `size="m"` (default)
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Переключатель среднего размера"
    checked={checked}
    onChange={onChange}
/>
```

#### `size="l"`
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Переключатель большого размера"
    size="l"
    checked={checked}
    onChange={onChange}
/>
```

#### `size="xl"`
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<Switch
    name="name"
    value="value"
    children="Переключатель очень большого размера"
    size="xl"
    checked={checked}
    onChange={onChange}
/>
```

## Многострочный
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<div style={{maxWidth: '600px'}}>
    <Switch
        name="name"
        value="value"
        children="Переключатель большого размера и с очень длинным текстом, который не вмещается в одну строчку"
        checked={checked}
        onChange={onChange}
    />
</div>
```

## Многострочный с align="top"
```jsx
const [checked, setChecked] = React.useState(false);
const onChange = ({currentTarget: {checked}}) => setChecked(checked);

<div style={{maxWidth: '600px'}}>
    <Switch
        name="name"
        value="value"
        align="top"
        children="Переключатель большого размера и с очень длинным текстом, который не вмещается в одну строчку"
        checked={checked}
        onChange={onChange}
    />
</div>
```

## Отступы друг от друга

#### `size="m"`
```jsx
const [checkedItems, setCheckedItems] = React.useState({
    checkedFirstItem: false,
    checkedSecondItem: true
});
const onChange = ({currentTarget: {checked, name}}) => setCheckedItems({
    ...checkedItems,
    [name]: checked,
});

<div>
    <Switch
        name="checkedFirstItem"
        value="value"
        children="Переключатель"
        checked={checkedItems.checkedFirstItem}
        onChange={onChange}
    />
    <Switch
        name="checkedSecondItem"
        value="value"
        children="Переключатель"
        checked={checkedItems.checkedSecondItem}
        onChange={onChange}
    />
</div>
```

#### `size="l"`
```jsx
const [checkedItems, setCheckedItems] = React.useState({
    checkedFirstItem: false,
    checkedSecondItem: true
});
const onChange = ({currentTarget: {checked, name}}) => setCheckedItems({
    ...checkedItems,
    [name]: checked,
});

<div>
    <Switch
        name="checkedFirstItem"
        value="value"
        size="l"
        children="Переключатель"
        checked={checkedItems.checkedFirstItem}
        onChange={onChange}
    />
    <Switch
        name="checkedSecondItem"
        value="value"
        size="l"
        children="Переключатель"
        checked={checkedItems.checkedSecondItem}
        onChange={onChange}
    />
</div>
```


