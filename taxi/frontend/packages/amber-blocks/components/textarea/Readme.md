Тип поля textarea

```jsx harmony
<Textarea
    rows={10}
    placeholder="Подсказка"
    theme="outline"
    value={state.value || ''}
    onClear={() => setState({value: ''})}
    onChange={value => setState({value})}
    clear
/>
```
