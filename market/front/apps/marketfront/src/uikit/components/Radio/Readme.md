### Песочница
```js noeditor
<Helper.Playground
    component={Radio}
    defaultValues={{label: 'беру!'}}
/>
```

### Примеры
#### `label`
Текстовое описание

```jsx
<Radio
    name="name"
    value="value"
    label="Переключатель 1"
    checked={true}
/>
```

#### `children`
*Если задать `label` и `children` одновременно, то приоритет будет у `label`*

```jsx
<Radio
    name="name"
    value="value"
    checked={true}
>
    <span>Я согласен не использовать <i>children</i> для сложных кейсов. </span>
    <a href="#">Подробнее</a>
</Radio>
```

#### `checked`

```jsx
const [checkedValue, setCheckedValue] = React.useState("2"); 
const onChange = ({currentTarget: {checked, value}}) => checked && setCheckedValue(value);

<div>
    <Radio
        name="example"
        value="1"
        checked={checkedValue === "1"}
        onChange={onChange}
        label="Радиокнопка 1"
    />
    <br/>
    <Radio
        name="example"
        value="2"
        checked={checkedValue === "2"}
        onChange={onChange}
        label="Радиокнопка 2"
    />
    <br/>
    <Radio
        name="example"
        value="3"
        checked={checkedValue === "3"}
        onChange={onChange}
        label="Радиокнопка 3"
    />
</div>
```

#### `disabled`

```jsx
const [checkedValue, setCheckedValue] = React.useState("2"); 
const onChange = ({currentTarget: {checked, value}}) => checked && setCheckedValue(value);

<div>
    <Radio
        name="example-disabled"
        value="1"
        checked={checkedValue === "1"}
        onChange={onChange}
        label="Радиокнопка 1"
        disabled
    />
    <br/>
    <Radio
        name="example-disabled"
        value="2"
        checked={checkedValue === "2"}
        onChange={onChange}
        label="Радиокнопка 2"
        disabled
    />
</div>
```

#### `size`
##### `size="m"` (default)

```jsx
const [checkedValue, setCheckedValue] = React.useState("2"); 
const onChange = ({currentTarget: {checked, value}}) => checked && setCheckedValue(value);

<div style={{maxWidth: '600px'}}>
    <Radio
        name="example-size-m"
        value="1"
        checked={checkedValue === "1"}
        onChange={onChange}
        label="Радиокнопка 1 с очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень длинным текстом, который не помещается в одну строку"
    />
    <br/>
    <Radio
        name="example-size-m"
        value="2"
        checked={checkedValue === "2"}
        onChange={onChange}
        label="Радиокнопка 2"
    />
    <br/>
    <Radio
        name="example-size-m"
        value="3"
        checked={checkedValue === "3"}
        onChange={onChange}
        label="Радиокнопка 3"
        disabled
    />
</div>
```

##### `size="l"`

```jsx
const [checkedValue, setCheckedValue] = React.useState("2"); 
const onChange = ({currentTarget: {checked, value}}) => checked && setCheckedValue(value);

<div style={{maxWidth: '600px'}}>
    <Radio
        name="example-size-l"
        value="1"
        checked={checkedValue === "1"}
        size="l"
        onChange={onChange}
        label="Радиокнопка 1 с очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень длинным текстом, который не помещается в одну строку"
    />
    <br/>
    <Radio
        name="example-size-l"
        value="2"
        checked={checkedValue === "2"}
        size="l"
        onChange={onChange}
        label="Радиокнопка 2"
    />
    <br/>
    <Radio
        name="example-size-l"
        value="3"
        checked={checkedValue === "3"}
        size="l"
        onChange={onChange}
        label="Радиокнопка 3"
        disabled
    />
</div>
```

##### `size="xl"`

```jsx
const [checkedValue, setCheckedValue] = React.useState("2"); 
const onChange = ({currentTarget: {checked, value}}) => checked && setCheckedValue(value);

<div style={{maxWidth: '600px'}}>
    <Radio
        name="example-size-xl"
        value="1"
        checked={checkedValue === "1"}
        size="xl"
        onChange={onChange}
        label="Радиокнопка 1 с очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень-очень длинным текстом, который не помещается в одну строку"
    />
    <br/>
    <Radio
        name="example-size-xl"
        value="2"
        checked={checkedValue === "2"}
        size="xl"
        onChange={onChange}
        label="Радиокнопка 2"
    />
    <br/>
    <Radio
        name="example-size-xl"
        value="3"
        checked={checkedValue === "3"}
        size="xl"
        onChange={onChange}
        label="Радиокнопка 3"
        disabled
    />
</div>
```


### `align`
Позиционирование радиокнопки. `baseline` старается центроваться по первой строке

```jsx
<div style={{maxWidth: '600px'}}>
    <div>
        <Radio
            name="checkedFirstItem"
            value="value"
            label="top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top top"
            align="top"
            checked={true}
        />
    </div>
    <br /><br />
    <div>
        <Radio
            name="checkedSecondItem"
            value="value"
            label="baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline baseline"
            align="baseline"
            checked={true}
        />
    </div>
    <br /><br />
    <div>
        <Radio
            name="checkedThirdItem"
            value="value"
            label="middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle middle"
            align="middle"
            checked={true}
        />
    </div>
</div>
```
