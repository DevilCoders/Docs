## Папка для брендовых цветов, стилей и т.п. других сервисов (таких как Сбербанк)

### Брендовые цвета других сервисов

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div style={{display: 'flex', flexWrap: 'wrap'}}>
        <BrandColor color="brand-yandex-yellow"/>
        <BrandColor color="brand-yandex-yellow-hover"/>
        <BrandColor color="brand-yandex-yellow-pressed"/>
        <BrandColor color="brand-yandex-coal-black"/>
        <BrandColor color="brand-yandex-red"/>
        <BrandColor color="brand-yandex-concrete-gray"/>
        <BrandColor color="brand-yandex-smoke-gray"/>
        <BrandColor color="brand-yandex-silver-gray"/>
        <BrandColor color="brand-yandex-gray-hover"/>
        <BrandColor color="brand-yandex-gray-pressed"/>
        <BrandColor color="brand-yandex-iron-gray"/>
        <BrandColor color="brand-yandex-ash-gray"/>
        <BrandColor color="brand-yandex-grass-green"/>
        <BrandColor color="brand-yandex-cobalt-blue"/>
        <BrandColor color="brand-yandex-wine-red"/>
        <BrandColor color="brand-yandex-electric-blue"/>
        <BrandColor color="brand-sber-green"/>
        <BrandColor color="brand-yandex-ya-pay"/>
        <BrandColor color="brand-yandex-ya-pay-hover"/>
    </div>
</Provider>
```

