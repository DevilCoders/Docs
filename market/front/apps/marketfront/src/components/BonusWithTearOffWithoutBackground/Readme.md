### Купон с отрывной частью и прозрачным фоном

```jsx

    const today = new Date();
    const bonus = {
        title: 'Бесплатная доставка',
        subtitle: 'Любого заказа',
        backgroundColor: '#16c67a',
        images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        endDate: today.setDate(today.getDate() + 1),
    };

    <div style={{width: 500}}>
        <div>
            <BonusWithTearOffWithoutBackground
                bonus={bonus}
            />
        </div>
    </div>
```
