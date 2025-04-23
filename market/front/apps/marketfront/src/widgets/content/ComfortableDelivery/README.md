## Overview

ComfortableDelivery отображает информацию о доставке.

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('./components/View/index.touch').default;
    const Desktop = require('./components/View/index.desktop').default;

    const ComfortableDelivery = createPlatformProxyComponent({Touch, Desktop});

    let store = createStore(() => {});

    <Provider store={store}>
        <ViewPort width={1200} height={600}>
            <ComfortableDelivery />
        </ViewPort>
    </Provider>
```
