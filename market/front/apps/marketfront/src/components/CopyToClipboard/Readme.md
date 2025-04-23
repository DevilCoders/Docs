Копирует текст в буфер обмена при клике на компонент.

#### Пример

```jsx

const Button = require('@self/root/src/uikit/components/Button').default;

const values = ['Первый', 'Второй', 'Третий', 'Четвертый'];

<div>
    {values.map(value => (
        <div style={{display:'inline-block', marginRight: '15px'}}>
            <CopyToClipboard
                text={value}
                onCopy={value => setState({value,})}
            >
                <Button>{value}</Button>
            </CopyToClipboard>
        </div>
    ))}

    <div style={{marginTop: '20px'}}>
        Текст в буфере обмена: <b>{state.value || '–'}</b>
    </div>
</div>
```
