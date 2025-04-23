### Виджет 'Попап купона'

Полученный купон

```jsx
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('@self/root/src/components/CoinPopup/View').default;
    const Desktop = require('@self/root/src/components/CoinPopup/View').default;
    const BonusPopup = createPlatformProxyComponent({Touch, Desktop});

    const bonus = {
        id: 1,
        title: 'Бесплатная доставка',
        subtitle: 'любого заказа',
        description: 'Электронику, одежду и средства для стирки вы теперь можете купить на 5% дешевле. Этот Маркет Бонус можно использовать отдельно или вместе с другими.',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: '01-01-2025',
    };

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <BonusPopup coin={bonus}/>
        </ViewPort>
    </Provider>
```

Купон, который можно получить

```jsx
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('@self/root/src/components/CoinPopup/View').default;
    const Desktop = require('@self/root/src/components/CoinPopup/View').default;
    const BonusPopup = createPlatformProxyComponent({Touch, Desktop});

    const bonus = {
        id: 1,
        promoId: 2,
        title: 'Бесплатная доставка',
        subtitle: 'любого заказа',
        description: 'Электронику, одежду и средства для стирки вы теперь можете купить на 5% дешевле. Этот Маркет Бонус можно использовать отдельно или вместе с другими.',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: '01-01-2025',
    };

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <BonusPopup coin={bonus}/>
        </ViewPort>
    </Provider>
```


Неактивный купон выданный за заказ

```jsx
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('@self/root/src/components/CoinPopup/View').default;
    const Desktop = require('@self/root/src/components/CoinPopup/View').default;
    const BonusPopup = createPlatformProxyComponent({Touch, Desktop});

    const bonus = {
        id: 1,
        status: 'INACTIVE',
        reason: 'ORDER',
        reasonParam: '1212',
        title: 'Бесплатная доставка',
        subtitle: 'любого заказа',
        description: 'Электронику, одежду и средства для стирки вы теперь можете купить на 5% дешевле. Этот Маркет Бонус можно использовать отдельно или вместе с другими.',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: '01-01-2025',
    };

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <BonusPopup coin={bonus}/>
        </ViewPort>
    </Provider>
```

Просроченный купон

```jsx
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('@self/root/src/components/CoinPopup/View').default;
    const Desktop = require('@self/root/src/components/CoinPopup/View').default;
    const BonusPopup = createPlatformProxyComponent({Touch, Desktop});

    const bonus = {
        id: 1,
        title: 'Бесплатная доставка',
        subtitle: 'любого заказа',
        description: 'Электронику, одежду и средства для стирки вы теперь можете купить на 5% дешевле. Этот Маркет Бонус можно использовать отдельно или вместе с другими.',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: '01-01-2015',
    };

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <BonusPopup coin={bonus}/>
        </ViewPort>
    </Provider>
```

```jsx noeditor
    document.body.style.overflow = 'auto';
```
