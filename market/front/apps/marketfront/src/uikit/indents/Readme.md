### Отступы синего маркета

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const arr = Array(13).fill(0);

<Provider store={store}>
    <div>
        {arr.map((v, i) => (
            <Indents value={`indent${i+1}`} />
        ))}
    </div>
</Provider>
```
