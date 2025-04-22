### Купон с отрывной частью контрол

```jsx

    const coin = {
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
    };

    initialState = {
        isChecked: false,
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffControl
                coin={coin}
                isChecked={state.isChecked}
                turnDirection='right'
                toggleCoin={() => setState({isChecked: !state.isChecked})}
            />
        </div>
        <div style={{marginTop: 20}}>
            <BonusWithTearOffControl
                coin={coin}
                isChecked={state.isChecked}
                turnDirection='left'
                toggleCoin={() => setState({isChecked: !state.isChecked})}
            />
        </div>
    </div>
```
