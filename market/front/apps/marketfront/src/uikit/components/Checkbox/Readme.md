### Песочница
```js noeditor
<Helper.Playground
    component={Checkbox}
    defaultValues={{label: 'беру!'}}
/>
```

### Примеры
### `label`
Текстовое описание

```jsx
const [checked, setChecked] = React.useState(false);

<Checkbox
    name="name"
    value="value"
    label="Переключатель 1"
    checked={checked}
    onChange={() => setChecked(!checked)}
/>
```

### `children`
Если задать `label` и `children` одновременно, то приоритет будет у `label`

```jsx
const [checked, setChecked] = React.useState(false);

<Checkbox
    name="name"
    value="value"
    checked={checked}
    onChange={() => setChecked(!checked)}
>
    <span>Я согласен не использовать <i>children</i> для сложных кейсов. </span>
    <a href="#">Подробнее</a>
</Checkbox>
```

### `checked`

#### `checked={false}` (default)
```jsx
const [checked, setChecked] = React.useState(false);


<Checkbox
    name="name"
    value="value"
    label="Выключенный переключатель"
    checked={checked}
    onChange={() => setChecked(!checked)}
/>
```

#### `checked={true}`
```jsx
const [checked, setChecked] = React.useState(false);


<Checkbox
    name="name"
    value="value"
    label="Включенный переключатель"
    checked={checked}
    onChange={() => setChecked(!checked)}
/>
```

### disabled
#### `disabled={false}` (default)
```jsx
const [checked, setChecked] = React.useState(false);

<Checkbox
    name="name"
    value="value"
    label="Переключатель"
    checked={checked}
    onChange={() => setChecked(!checked)}
/>
```

#### `disabled={true}`
```jsx
const [checkedFirstItem, setCheckedFirstItem] = React.useState(false);
const [checkedSecondItem, setCheckedSecondItem] = React.useState(true);

<div style={{maxWidth: '600px'}}>
    <Checkbox
        name="name"
        value="value"
        label="Неактивный переключатель"
        checked={checkedFirstItem}
        disabled={true}
        onChange={() => setCheckedFirstItem(!checkedFirstItem)}
    />
    <Checkbox
        name="name"
        value="value"
        label="Активный переключатель"
        checked={checkedSecondItem}
        disabled={true}
        onChange={() => setCheckedSecondItem(!checkedSecondItem)}
    />
</div>
```

### `size`

#### `size="m"` (default)
```jsx
const [checkedFirstItem, setCheckedFirstItem] = React.useState(false);
const [checkedSecondItem, setCheckedSecondItem] = React.useState(true);

<div style={{maxWidth: '600px'}}>
    <Checkbox
        name="name"
        value="value"
        label="Чекбокс с очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень длинным текстом, который не помещается в одну строку"
        checked={checkedFirstItem}
        onChange={() => setCheckedFirstItem(!checkedFirstItem)}
    />
    <Checkbox
        name="name"
        value="value"
        label="Переключатель"
        checked={checkedSecondItem}
        onChange={() => setCheckedSecondItem(!checkedSecondItem)}
    />
</div>
```

#### `size="l"`
```jsx
const [checkedFirstItem, setCheckedFirstItem] = React.useState(false);
const [checkedSecondItem, setCheckedSecondItem] = React.useState(true);

<div style={{maxWidth: '600px'}}>
    <Checkbox
        name="name"
        value="value"
        size="l"
        label="Чекбокс с очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень длинным текстом, который не помещается в одну строку"
        checked={checkedFirstItem}
        onChange={() => setCheckedFirstItem(!checkedFirstItem)}
    />
    <Checkbox
        name="name"
        value="value"
        size="l"
        label="Переключатель"
        checked={checkedSecondItem}
        onChange={() => setCheckedSecondItem(!checkedSecondItem)}
    />
</div>
```

### `theme`

```jsx
const [checkedFirstItem, setCheckedFirstItem] = React.useState(false);
const [checkedSecondItem, setCheckedSecondItem] = React.useState(true);

<div style={{maxWidth: '600px'}}>
    <div>
        <Checkbox
            name="name"
            value="value"
            label="Тема normal"
            checked={checkedFirstItem}
            onChange={() => setCheckedFirstItem(!checkedFirstItem)}
        />
    </div>
    <div>
        <Checkbox
            name="name"
            value="value"
            label="Тема muted"
            checked={checkedSecondItem}
            theme="muted"
            onChange={() => setCheckedSecondItem(!checkedSecondItem)}
        />
    </div>
</div>
```


### `align`
Позиционирование чекбокса. `baseline` старается центроваться по первой строке

```jsx
const [checkedFirstItem, setCheckedFirstItem] = React.useState(true);
const [checkedSecondItem, setCheckedSecondItem] = React.useState(true);
const [checkedThirdItem, setcheckedThirdItem] = React.useState(true);

<div style={{maxWidth: '600px'}}>
    <div>
        <Checkbox
            name="name"
            value="value"
            label="top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top"
            align="top"
            checked={checkedFirstItem}
            onChange={() => setCheckedFirstItem(!checkedFirstItem)}
        />
    </div>
    <br /><br />
    <div>
        <Checkbox
            name="name"
            value="value"
            label="baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline"
            align="baseline"
            checked={checkedSecondItem}
            onChange={() => setCheckedSecondItem(!checkedSecondItem)}
        />
    </div>
    <br /><br />
    <div>
        <Checkbox
            name="name"
            value="value"
            label="middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle"
            align="middle"
            checked={checkedThirdItem}
            onChange={() => setcheckedThirdItem(!setcheckedThirdItem)}
        />
    </div>
</div>
```
