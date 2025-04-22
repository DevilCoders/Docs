Радио группа

Пример использования:
```jsx
const {RadioInput, CheckedLabel} = require('@self/platform/components/RadioGroup');

const initialState = {value: null};
const [state, setState] = React.useState(initialState);
<RadioGroup
    name="colorPicker"
    value={state.value}
    onChange={(value) => setState({value})}
    onReset={() => setState({value: null})}
>
    <CheckedLabel label="Выбранный стул" />
    <RadioInput value="one">One</RadioInput>
    <RadioInput value="two">Two</RadioInput>
</RadioGroup>
```

Можно стилизовать:
```jsx
const {RadioInput} = require('@self/platform/components/RadioGroup');

const initialState = {value: null};
const [state, setState] = React.useState(initialState);
<RadioGroup
    name="sizePicker"
    value={state.value}
    onChange={(value) => setState({value})}
    onReset={() => setState({value: null})}
>
    <div style={{display: 'flex', flexDirection: 'column'}}>
        <div style={{margin: '10px', color: 'red'}}>
            <RadioInput value="one">One</RadioInput>
        </div>
        <div style={{margin: '10px'}}>
            <RadioInput value="two">Two</RadioInput>
        </div>
    </div>
</RadioGroup>
```
