Чекбокс

Пример использования:
```jsx
const Checkbox = require('@self/platform/components/Control/Checkbox').default;

const initialState = {value: false};

<Checkbox
  title="Memes"
  isChecked={state.value}
  onChange={() => setState({value: !state.value})}
/>
```
