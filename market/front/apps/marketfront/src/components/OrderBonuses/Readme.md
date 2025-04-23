### Купоны за заказ

```jsx
    import OrderBonuses from '@self/root/src/components/OrderBonuses';

    import {Provider} from 'react-redux';
    import {createStore} from 'redux';

    const coin = {
        id: 1,
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    const coin2 = {
        id: 2,
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        };

    const coin3 = {
        id: 3,
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    const coin4 = {
        id: 4,
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        };

    const coin5 = {
        id: 5,
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        };

    const store = createStore(() => ({
        collections: {
            coin: {
                1: coin,
                2: coin2,
                3: coin3,
                4: coin4,
                5: coin5,
            }
        },
    }));

    const coinIds = [1, 2, 3, 4, 5];

    <Provider store={store}>
        <OrderBonuses coinIds={coinIds} />
    </Provider>
```
