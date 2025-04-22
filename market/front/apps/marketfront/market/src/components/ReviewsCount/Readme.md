```jsx noeditor
import ReviewsCount from '@self/project/src/components/ReviewsCount';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground component={ReviewsCount} />
</Provider>
```
