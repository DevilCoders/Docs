### Элемент ScrollBox'a
Ссылка с картинкой и подписью.
(Используются cms-ные стили)

```jsx
import Navnode from '@self/root/src/components/Navnode';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const mockProps = {
    url: "/catalog--elektronika/54440",
    image: '//avatars.mds.yandex.net/get-mpic/466729/cms_resources-navigation-pages-48495-deb19851534ebba1ad3aba9e7c10d4c8.png/optimize',
    name: 'Электроника',
};

<Provider store={store}>
    <Helper.Playground
        component={Navnode}
        defaultValues={mockProps}
    />
</Provider>
```
