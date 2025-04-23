Тумблер
```jsx

initialState = {checked: false};
const toggle = () => setState(({checked}) => ({checked: !checked}));

<Tumbler
    checked={state.checked}
    onChange={toggle}
/>
```
