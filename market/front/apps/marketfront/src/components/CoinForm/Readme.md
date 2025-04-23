### Форма для пустого Купона

В коллекции купонов нужен компонент, который представляет собой блок, который по-форме выглядит как бонус.

```jsx
import CoinEmpty from '.';

const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

let store = createStore(() => {});

<Provider store={store}>
  <CoinEmpty />
</Provider>
```
