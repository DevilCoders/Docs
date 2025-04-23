Поле с маской ввода. Используется библиотека [react-input-mask](https://github.com/sanniassin/react-input-mask)

```jsx harmony
<InputMask
    mask="+7 (999)-999-99-99"
    placeholder="+7 (999)-999-99-99"
    theme="outline"
    value={state.value || ''}
    onClear={() => setState({value: ''})}
    onChange={value => setState({value})}
    clear
/>
```
