
## Примеры

### Cпособ получения саджестов(без сносок)
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import {Suggest as SuggestView} from '.';

const store = createStore(() => ({
    collections: {},
}));

const fetchSuggestions = () => Promise.resolve(
[
    {name: 'Москва'},
    {name: 'Владивосток'}
]
);

<Provider store={store}>
    <SuggestView label='Город' valueKey='name' fetchSuggestions={fetchSuggestions} />
</Provider>
```
