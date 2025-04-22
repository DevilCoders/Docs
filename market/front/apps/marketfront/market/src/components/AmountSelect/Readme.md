```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    amount: 1,
};

<Provider store={store}>
    <Helper.Playground
        component={AmountSelect}
        defaultValues={{amount: state.amount}}
        settings={{background: 'transparent'}}
        example={props => (
            <AmountSelect
                {...props}
                amount={state.amount}
                onChange={amount => setState({amount})}
            />
        )}
    />
</Provider>
```
