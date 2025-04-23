### Песочница
```js noeditor
<Helper.Playground
    component={RadioButton}
    defaultValues={{children: 'беру!'}}
/>
```

##№ Параметры
### `label`
Текстовое описание

```jsx
const name = 'example-radio-button';

<RadioButton
    name={name}
    value="value"
    label="Переключатель 1"
    checked={true}
    width='auto'
/>
```

### `children`
*Если задать `label` и `children` одновременно, то приоритет будет у `label`*

```jsx
    import Text from '@self/root/src/uikit/components/Text';
    const [idChecked, setIdChecked] = React.useState('');

    const onChange = event => setIdChecked(event.target.value);

    const boxContentStyle = {width: '200px'};
    const boxWrapperStyle = {display: 'flex'};

    <div style={boxWrapperStyle}>
        <RadioButton
            checked={idChecked === 'radio1'}
            id='radio1'
            name='radioBox'
            value='radio1'
            disabled={true}
            onChange={onChange}
        >
                {'Переключатель 1'}
        </RadioButton>
        <RadioButton
            checked={idChecked === 'radio2'}
            id='radio2'
            name='radioBox'
            value='radio2'
            onChange={onChange}
        >
                {'Переключатель 2'}
        </RadioButton>
        <RadioButton
            checked={idChecked === 'radio3'}
            id='radio3'
            name='radioBox'
            value='radio3'
            onChange={onChange}
        >
                {'Переключатель 3'}
        </RadioButton>
        <RadioButton
            checked={idChecked === 'radio4'}
            id='radio4'
            name='radioBox'
            value='radio4'
            onChange={onChange}
        >
            <div style={boxContentStyle}>
                {'Переключатель 4'}
                <div>
                    <Text theme='muted'>Вложенный элемент с форматированием</Text>
                </div>
            </div>
        </RadioButton>
    </div>
```
