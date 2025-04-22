### Панель Купонов

```jsx
import Title from '@self/root/src/uikit/components/Title';
const {$green600, $purple600} = require('@self/root/src/uikit/palette/colors');

const coins = [{
    id: 1,
    title: 'Бесплатная доставка',
    subtitle: 'любого заказа',
    backgroundColor: $green600,
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'}
}, {
    id: 2,
    title: 'Скидка 5%',
    subtitle: 'на категорию «Бытовая техника для кухни»',
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
}, {
    id: 3,
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
}, {
    id: 4,
    title: 'Бесплатная доставка',
    subtitle: 'любого заказа',
    backgroundColor: $purple600,
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'}
}, {
    id: 5,
    title: 'Скидка 5%',
    subtitle: 'на категорию «Бытовая техника для кухни»',
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
}, {
    id: 6,
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
}];

const CoinComponent = require('@self/root/src/uikit/components/Coin').default;

<div>
    <CoinPane
        coins={coins}
        fade={false}
        CoinComponent={CoinComponent}
    />

    <Title size={500}>Fade: true</Title>

    <CoinPane coins={coins} fade={true} CoinComponent={CoinComponent} />
</div>
```
