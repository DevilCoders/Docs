Радиобокс
```jsx
const radiobox = ctx.Radiobox({state, setState, checked: 'YES'});

const {initialState, onChange} = radiobox;

<Radiobox
    name='testBox'
    onChange={onChange}
    buttons={[{
        label: 'Checked',
        value: 'YES',
        checked: radiobox.value === 'YES',
    }, {
        label: 'Disabled',
        value: 'NO',
        checked: radiobox.value === 'NO',
        disabled: true,
    }, {
        label: 'Unchecked',
        value: 'ANOTHER',
        checked: radiobox.value === 'ANOTHER',
    }, {
        label: 'Checked-disabled',
        value: 'OTHER',
        checked: true,
        disabled: true,
    }]}
/>
```

Можно расположить кнопки вертикально, передав проп `direction="column"`

```jsx
const radiobox = ctx.Radiobox({state, setState, checked: 'YES'});

const {initialState, onChange} = radiobox;

<Radiobox
    name='testBox'
    direction="column"
    onChange={onChange}
    buttons={[{
        label: 'Checked',
        value: 'YES',
        checked: state.checked === 'YES',
    }, {
        label: 'Disabled',
        value: 'NO',
        checked: state.checked === 'NO',
        disabled: true,
    }, {
        label: 'Unchecked',
        value: 'ANOTHER',
        checked: state.checked === 'ANOTHER',
    }, {
        label: 'Checked-disabled',
        value: 'OTHER',
        checked: true,
        disabled: true,
    }]}
/>
```
