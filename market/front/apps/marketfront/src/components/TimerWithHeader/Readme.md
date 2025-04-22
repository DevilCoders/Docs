
## Примеры

### Таймер с обратным осчетом в widgetWrapper с динамическим title
```jsx
import dayjs from 'dayjs';

const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

let store = createStore(() => {});

<Provider store={store}>
    <Helper.Playground
        component={TimerWithHeader}
        defaultValues={{
            title: 'title middle',
            titleBeforeStart: 'title before',
            titleAfterEnd: 'title after',
            dateTimeStart: Number(new Date()) + 5000,
            dateTimeEnd: Number(new Date()) + 15000,
        }}
    />
</Provider>
```
