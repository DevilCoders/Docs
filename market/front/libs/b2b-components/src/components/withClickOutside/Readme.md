Добавляет хендлер `onOutsideClick`, который вызывается при клике снаружи компонента.

```jsx
const {default: withClickOutside} = require('./')
initialState = {count: 0}

const Content = () => <div>count: {state.count}</div>

const Enhanced = withClickOutside(Content)

;
<Enhanced onOutsideClick={() => setState(({count}) => ({count: count + 1}))} />
```
