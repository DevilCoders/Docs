Компонент показа переданных элементов, с построчной или табличной разбивкой с лимитированным колличеством

```jsx
import ClampItems from '@self/root/src/components/ClampItems';
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const lorem = num => helper.generateText({words: (num + 1) * 2});

<Provider store={store}>
    <Helper.Playground
        component={ClampItems}
        settings={{background: 'transparent'}}
        forceUpdate={true}
        example={(props) => {
            const children = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25].map((it, i) => <div>Итем {it} {lorem(i)} </div>);

            return <ClampItems {...props}>{children}</ClampItems>

        }}
    />
</Provider>
