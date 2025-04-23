### Компонент, в котором сообщается что купоны в случае отмены будут утеряны

```jsx
    const bonuses= [
        {
            subtitle: 'слышь, чо',
            description: 'через плечо',
            images: {
                standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/9853f140-b085-487a-b822-ef4bdf852b03/',
            },
            title: 'Скидка 1000 ₽',
            backgroundColor: '#808080',
        },
        {
            title: 'Бесплатная доставка',
            subtitle: 'Любого заказа',
            backgroundColor: '#16c67a',
            images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        }
    ];

    <div style={{width: 335}}>
        <BonusesWillLost
            bonuses={bonuses}
            onBackButtonClickHandler={() => {alert('Вы нажали кнопку "Вернуться"')}}
            onContinueButtonClickHandler={() => {alert('Вы нажали кнопку "Продолжить"')}}
        />
    </div>
```

Можно добавить спиннер на кнопку "Продолжить"

```jsx
    const bonuses= [
        {
            subtitle: 'слышь, чо',
            description: 'через плечо',
            images: {
                standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/9853f140-b085-487a-b822-ef4bdf852b03/',
            },
            title: 'Скидка 1000 ₽',
            backgroundColor: '#808080',
        },
        {
            title: 'Бесплатная доставка',
            subtitle: 'Любого заказа',
            backgroundColor: '#16c67a',
            images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
        }
    ];

    <div style={{width: 335}}>
        <BonusesWillLost
            bonuses={bonuses}
            isProcessing
            onBackButtonClickHandler={() => {alert('Вы нажали кнопку "Вернуться"')}}
            onContinueButtonClickHandler={() => {alert('Вы нажали кнопку "Продолжить"')}}
        />
    </div>
```
