Поле ввода текстовых данных.


```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const InformationPanel = require('@self/root/src/components/InformationPanel').default;

<Provider store={store}>
    <div style={{display: 'inline-block'}}>
        <InformationPanel theme={'success'} icon='info' withTail={true}>
            <InformationPanel.Title>
                В новых проектах используем `view = normal`.
            </InformationPanel.Title>
        </InformationPanel>
    </div>
</Provider>
```

### Песочница
```jsx noeditor
<Helper.Playground
    component={TextField}
    forceUpdate={true}
    defaultValues={{
        label: 'Заголовок',
        view: 'normal',
        size: 'l',
    }}
/>
```

### Параметры

#### `autofocus`

Boolean параметр, который ставит фокус при рендере.

```jsx
<TextField view='normal' size="l" autofocus={true} label="Поле с автофокусом" />
```

#### `disabled`

Boolean параметр, который включает неактивное состояние поля ввода.

```jsx
<TextField view='normal' size="l" disabled={true} value="Я недоступно" label="Недоступное поле" />
```

#### `isValidated`

Boolean параметр, который показывает, что значение в филде завалидировано

```jsx
<TextField size="l" view='normal' isValidated={true} value="Я провалидировано" label="Валидное поле"/>
```

#### `rows`
На сколько строк нужен инпут. `1` - по умолчанию

```jsx
const [value, setValue] = React.useState('')
const onChange = event => {
    setValue(event.target.value);
};

<TextField  size="l" view='normal' value={value} rows="2" onChange={onChange} label="Поле для длинных текстов, нужно дорабатывать для корректного отображения" />
```

```jsx
const [value, setValue] = React.useState('')
const onChange = event => {
    setValue(event.target.value);
};

<TextField size="l" view='normal' value={value} rows="1" maxRows="50" onChange={onChange} label="Расширяющееся поле для длинных текстов" />
```


#### Тема

`error`

```jsx
const [state, setState] = React.useState({
    value: 'Ошибка',
    view: 'error',
})
const onChange = event => {
    setState({
        value: event.target.value,
        view: 'normal'
    });
};
const onClear = event => {
    setState({ value: '' });
};

<TextField size="l" view='normal' theme={state.view} value={state.value} onChange={onChange} onClear={onClear} label="Поле с темой error"/>
```
#### `size`

```jsx
const Button = require('@self/root/src/uikit/components/Button').default;

<div>
    <div>
        <TextField view='normal' size="l" label="Большое поле"/>
    </div>

    <div style={{marginTop: '20px'}}>
        <TextField view='normal' size="m" label="Обычное поле"/>
    </div>

    <div style={{marginTop: '20px'}}>
        <TextField view='normal' size="s" label="Маленькое поле"/>
    </div>

    <div style={{marginTop: '20px'}}>
        <TextField view='normal' size="xs" label="Ещё меньше"/>
    </div>

    <div style={{marginTop: '20px', display: 'flex'}}>
        <Button size="l" pin="round-brick">Кнопа</Button>
        <TextField view='normal' pin="clear-clear" size="l" label="Большое поле"/>
        <Button size="l" pin="brick-round">Кнопа</Button>
    </div>

    <div style={{marginTop: '20px', display: 'flex'}}>
        <Button size="m" pin="round-brick">Кнопа</Button>
        <TextField view='normal' pin="clear-clear" size="m" label="Обычное поле"/>
        <Button size="m" pin="brick-round">Кнопа</Button>
    </div>

    <div style={{marginTop: '20px', display: 'flex'}}>
        <Button size="s" pin="round-brick">Кнопа</Button>
        <TextField view='normal' pin="clear-clear" size="s" label="Маленькое поле"/>
        <Button size="s" pin="brick-round">Кнопа</Button>
    </div>

    <div style={{marginTop: '20px', display: 'flex'}}>
        <Button size="xs" pin="round-brick">Кнопа</Button>
        <TextField view='normal' pin="clear-clear" size="xs" label="Ещё меньше"/>
        <Button size="xs" pin="brick-round">Кнопа</Button>
    </div>
</div>
```

#### `onClear`
При наличии показывает крестик в поле для очистки контента

```jsx
const [state, setState] = React.useState({
    value: 'Ошибка',
    view: '',
})
const onChange = event => {
    setState({
        value: event.target.value,
        view: 'normal'
    });
};
const onClear = event => {
    setState({ value: '' });
};

<div>
    <TextField view='normal'
        size="l"
        value={state.value}
        onChange={onChange}
        label="Без креста"
    />
    <br/>

    <TextField view='normal'
        size="l"
        value={state.value}
        onChange={onChange}
        onClear={onClear}
        label="С крестом"
    />
    <br/>

    <TextField view='normal'
        size="l"
        value={state.value}
        onChange={onChange}
        onClear={onClear}
        showClearOnlyFocused
        label="С крестом при фокусе"
    />
    <br/>

    <TextField view='normal'
        size="s"
        value={state.value}
        onChange={onChange}
        onClear={onClear}
        label="Маленький инпут с крестом"
    />
    <br/>

    <TextField view='normal'
        size="xs"
        value={state.value}
        onChange={onChange}
        onClear={onClear}
        label="Очень маленький инпут с крестом"
    />
</div>
```

### `value` и `defaultValue`

- Если передать `defaultValue` в компонент, и не передавать `value`,
  то он станет [uncontrolled component](https://nda.ya.ru/3UYREk)
- Если передать `value` в компонент, то он станет [controlled component](https://nda.ya.ru/3UYREg)

```jsx harmony
const [value, setValue] = React.useState('')
const onChange = event => {
    setValue(event.target.value);
};
const onClear = event => {
    setValue('');
};

<div>
    Текст в стейте: {value}
    <br/>
    <TextField view='normal'
        size="l"
        defaultValue={value}
        onChange={onChange}
        onClear={onClear}
        label="defaultValue"
    />
    <br/>
    <TextField view='normal'
        size="l"
        value={value}
        onChange={onChange}
        onClear={onClear}
        label="value"
    />
</div>
```

#### `magnifierInFront`
Лупа спереди



```jsx
const [state, setState] = React.useState({
    value: 'текст',
    view: '',
})
const onChange = event => {
    setState({
        value: event.target.value,
        view: 'normal'
    });
};

const onClear = event => {
    setState({ value: '' });
};

<div>
    <TextField
        view='normal'
        size="s"
        value={state.value}
        label="Без креста"
        withMagnifierControl
    />
    <br />
    <TextField
        view='normal'
        size="s"
        value={state.value}
        label="Без креста"
        withMagnifierControl
        magnifierInFront
    />
    <br />
    <TextField
        view='normal'
        size="s"
        value={state.value}
        label="С крестом"
        withMagnifierControl
        magnifierInFront
        onChange={onChange}
        onClear={onClear}
    />
    <br />
    <TextField
        view='normal'
        size="s"
        value={state.value}
        label="С маленьким крестом"
        withMagnifierControl
        magnifierInFront
        onChange={onChange}
        onClear={onClear}
        smallCleareButton
    />
</div>
```

#### `characterLimit`

Устанавливает нежёсткий лимит символов, который при желании можно превысить.

Добавляет счётчик, если количество символов превышает либо равно половине лимита.
Подкрашивает счётчик красным, если количество символов превысило лимит.

```jsx
const [value, setValue] = React.useState('Перебрал')
const onChange = event => {
    setValue(event.target.value);
};

<TextField value={value} characterLimit={10} onChange={onChange} />
```

```jsx
const [value, setValue] = React.useState('Перебрал с длиной текста')
const onChange = event => {
    setValue(event.target.value);
};

<TextField value={value} characterLimit={10} onChange={onChange} />
```

Также работает и с авто-расширяемым полем

```jsx
const [value, setValue] = React.useState('lorem ipsum dolor s')
const onChange = event => {
    setValue(event.target.value);
};

<TextField value={value} rows="1" maxRows="3" characterLimit={20} onChange={onChange} />
```
