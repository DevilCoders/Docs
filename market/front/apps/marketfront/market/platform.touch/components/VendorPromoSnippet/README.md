### Примеры


#### Вид с характеристиками

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => {});

    <Provider store={store}>  
        <VendorPromoSnippet
            productId={1}
            shortSpec="QLED, 49.9'"
            pictureProps={{
                src: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
                srcSet: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
            }}
            link={{
                params: {}
            }}
            prices={{
                min: '666000',
                currency: 'RUB',
            }}
        /> 
    </Provider>
```


#### Вид с названием модели

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => {});

    <Provider store={store}>  
        <VendorPromoSnippet
            productId={1}
            title="Панель панельная XYZ-2000"
            pictureProps={{
                src: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
                srcSet: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
            }}
            link={{
                params: {}
            }}
            prices={{
                min: '666000',
                currency: 'RUB',
            }}
        /> 
    </Provider>
```


#### Вид с названием модели и характеристиками

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => {});

    <Provider store={store}>  
        <VendorPromoSnippet
            productId={1}
            title="Панель панельная XYZ-2000"
            shortSpec="QLED, 49.9'"
            pictureProps={{
                src: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
                srcSet: "https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq",
            }}
            link={{
                params: {}
            }}
            prices={{
                min: '666000',
                currency: 'RUB',
            }}
        /> 
    </Provider>
```
