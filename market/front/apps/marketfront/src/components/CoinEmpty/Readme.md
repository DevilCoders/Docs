### Пустой Купон

#### size '400'
```jsx
import CoinEmpty from '@self/root/src/components/CoinEmpty';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground
        component={CoinEmpty}
    />
</Provider>

```
