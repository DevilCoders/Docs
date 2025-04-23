### Песочница
```js noeditor
import Phone from '@self/root/src/components/Phone';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const themes = 'normal, dark, light, gray, purple, black, white'.split(', ');

<Provider store={store}>
    <Helper.Playground
        component={Phone}
        props={{
            theme: {
                required: false,
                type: 'enum',
                values: themes
            }
        }}
    />
</Provider>

```
