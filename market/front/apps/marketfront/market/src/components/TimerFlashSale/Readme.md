
## Примеры

### TimerFlashSale

Используется для быстрых распродаж

```jsx
import dayjs from 'dayjs';
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div style={{textAlign: 'center'}}>
        <TimerFlashSale endTime={dayjs().add(100, 'second').format()} />
        <TimerFlashSale startTime={dayjs().add(10, 'second').format()} endTime={dayjs().add(100, 'second').format()} />
        <TimerFlashSale endTime={dayjs().add(100, 'minute').format()} size='widget'/>
    </div>
</Provider>
```
