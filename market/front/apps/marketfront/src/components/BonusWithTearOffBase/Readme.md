### Купон с отрывной частью базовый

```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const InformationPanel = require('@self/root/src/components/InformationPanel').default;

<div>
    <br/>

    <Provider store={store}>
        <InformationPanel theme='warning' icon='info'>
            <InformationPanel.Title>
                Компонент является базовым для BonusWithTearOff, BonusWithTearOffControl и BonusWithTearOffWithoutBackground. В продуктовом коде необходимо использовать именно их.
            </InformationPanel.Title>
        </InformationPanel>
    </Provider>
    <br/>
</div>

```

```jsx

    const coin = {
        title: 'Бесплатная доставка очень длинный заголовок очень длинный заголовок',
        subtitle: 'Любого заказа очень длинное описание очень длинное описание',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffBase
                coin={coin}
            />
        </div>
    </div>
```

Фон

```jsx

    const coin = {
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffBase
                coin={coin}
                withBackground={false}
            />
        </div>
    </div>
```

Отрывной купон

```jsx

    const coin = {
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffBase
                coin={coin}
                turnDirection='right'
            />
        </div>
        <div style={{marginTop: 20}}>
            <BonusWithTearOffBase
                coin={coin}
                turnDirection='left'
            />
        </div>
    </div>
```

Отрывной Купон с датой истечения

```jsx

    const coin = {
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: '25-12-2019 03:00:00',
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffBase
                coin={coin}
                turnDirection='right'
            />
        </div>
        <div style={{marginTop: 20}}>
            <BonusWithTearOffBase
                coin={coin}
                turnDirection='left'
            />
        </div>
    </div>
```
