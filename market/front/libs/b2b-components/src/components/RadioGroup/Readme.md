Радиогруппа с кнопками
```jsx

const Button = require('./Items/Button').default;

const radioGroup = ctx.RadioGroup({state, setState, checked: 'YES'});

const {initialState, onRadioGroupItemChange} = radioGroup;

<RadioGroup onRadioGroupItemChange={onRadioGroupItemChange} checked={state.checked}>
    <Button value="YES">Checked</Button>
    <Button value="NO" disabled>Disabled</Button>
    <Button value="ANOTHER">Unchecked</Button>
    <Button value="OTHER" checked={true} disabled>Checked-disabled</Button>
</RadioGroup>
```

Радиогруппа с кастомными переключателями
```jsx

const radioGroup = ctx.RadioGroup({state, setState, checked: 'YES'});

const {initialState, onRadioGroupItemChange} = radioGroup;

const defaultStyles = {cursor: 'pointer', marginRight: 10, padding: 10};
const Toggler = ({
    onRadioGroupItemChange,
    value,
    checked,
    children,
}) => (
    <div
        onClick={() => onRadioGroupItemChange(value)}
        style={checked ? Object.assign({}, defaultStyles, {borderBottom: '2px solid #f00'}) : defaultStyles}
    >
        {children}
    </div>
);

<RadioGroup onRadioGroupItemChange={onRadioGroupItemChange} checked={state.checked}>
    <Toggler value="YES">Checked</Toggler>
    <Toggler value="NO">Unchecked</Toggler>
</RadioGroup>
```
