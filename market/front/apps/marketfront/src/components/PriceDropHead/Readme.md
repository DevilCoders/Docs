### хедер прайсдропа


```jsx noeditor
import PriceDropHead from '@self/root/src/components/PriceDropHead';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {
        offer: {
            1: {
                id: '1',
            },
        },
    },
}));

<Provider store={store}>
    <PriceDropHead
        type="l"
        text="Этот товар снизил цены на другие — вот они"
        offerId="1"
    />
</Provider>
```
