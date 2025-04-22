### Элемент ScrollBox'a
Показывает лого производителя.

```jsx
import Vendor from '@self/root/src/components/Vendor';
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground
        component={Vendor}
        defaultValues={{
            brandLogo: "https://avatars.mds.yandex.net/get-mpic/397397/img_id2731930379172281406.png/orig",
            brandSlug: "Lego",
            brandId: 1234,
        }}
    />
</Provider>
```
