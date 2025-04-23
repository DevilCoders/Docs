### BankAccountForm
 
Компонент для ввода банковских реквизитов пользователя.

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground component={BankAccountForm} />
</Provider>
```
