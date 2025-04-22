```jsx harmony
<Checkbox
    label="Жми меня"
    checked={state.checked || false}
    onChange={() => setState({ checked: !state.checked })}
/>
```
Чекбокс с ошибкой
```jsx harmony
<Checkbox
    error
    label="Жми меня"
    checked={state.checked || false}
    onChange={() => setState({ checked: !state.checked })}
/>
```
Несколько строк
```jsx harmony
<div style={{width: '200px'}}>
    <Checkbox
        label="Очень длинная подпись чекбокса на несколько строк"
        checked={state.checked || false}
        onChange={() => setState({ checked: !state.checked })}
    />
</div>
```

Disabled
```jsx harmony
<Checkbox
    label="Жми меня"
    disabled
    checked={state.checked || false}
    onChange={() => setState({ checked: !state.checked })}
/>
```

Disabled - checked
 ```jsx harmony
<Checkbox
    label="Жми меня"
    disabled
    checked={state.checked || true}
    onChange={() => setState({ checked: !state.checked })}
/>
```

Indeterminate
 ```jsx harmony
initialState = {checked: true};
<>
    <Checkbox
        label="Жми меня"
        checked={state.checked || false}
        onChange={() => setState({ checked: !state.checked })}
    />
    {' '}
    <Checkbox label="indeterminate" indeterminate={state.checked}/>
</>
```

No label
```jsx harmony
<Checkbox
    checked={state.checked || false}
    onChange={() => setState({ checked: !state.checked })}
/>
```
