### Иконка приложения

Тянется по размеру контейнера

```js noeditor
import AppIcon from '@self/root/src/components/AppIcon';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div style={{width: 128, height: 128}}>
        <AppIcon />
    </div>
</Provider>

```
