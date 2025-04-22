### Показывает причины для покупки

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const reasons = [
    {
        id: "customers_choice",
        value: 0.92,
    }
];

<Provider store={store}>
    <div>
        <ReasonsToBuyList reasonsToBuy={reasons} />
    </div>
</Provider>
```

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const reasons = [
    {
        factor_name: "Объем памяти",
        type: "consumerFactor",
        factor_id: "745",
        value: 0.9809848666,
        factor_priority: "1",
        id: "best_by_factor"
    },
];

<Provider store={store}>
    <div>
        <ReasonsToBuyList reasonsToBuy={reasons} showBestFactor />
    </div>
</Provider>
```

### Показывает причину "Алиса живёт здесь"
```jsx
const reasons = [
    {
        id: "alisa_lives_here",
    }
];

<div>
    <ReasonsToBuyList reasonsToBuy={reasons} />
</div>
```

### Показывает причину "Работает с Алисой"
```jsx
const reasons = [
    {
        id: "compatible_with_alisa",
    }
];

<div>
    <ReasonsToBuyList reasonsToBuy={reasons} />
</div>
```
