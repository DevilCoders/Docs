Доопределение леговского `TextArea`, добавляет `error` и `className`
```(jsx)

initialState = {
    text: '',
};

const { TextArea } = require('./TextArea');

<TextArea
    cols={10}
    rows={5}
    size="m"
    theme="normal"
    hasClear
    text={state.text}
    onChange={(event) => setState({ text: event.target.value })}    
/>
```

```(jsx)
initialState = {
    text: '',
};

const { TextArea } = require('./TextArea');
<TextArea
    cols={10}
    rows={5}
    size="m"
    theme="normal"
    hasClear
    error={!Boolean(state.text)}
    text={state.text}
    onChange={(event) => setState({ text: event.target.value })} 
/>
```

```(jsx)

initialState = {
    text: '',
};

const { TextArea } = require('./TextArea');
<TextArea
    cols={10}
    rows={5}
    size="m"
    theme="normal"
    hasClear
    error={state.text ? false: "Необходимо ввести имя"}
    text={state.text}
    onChange={(event) => setState({ text: event.target.value })} 
/>
```
