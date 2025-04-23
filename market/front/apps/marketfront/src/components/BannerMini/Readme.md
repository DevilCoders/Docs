### Версточная обертка для баннера @self/root/src/components/Banner, чтобы он хорошо вставал, например, в ScrollBox
```jsx
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
<div>
    <BannerMini
        link="#"
        height={10}
        width={10}
        src='//avatars.mds.yandex.net/get-marketcms/475644/img-2a2a4c7b-d4d9-4c57-9b61-094b27cba55a.png/optimize'
    />
</div>
</Provider>
```
