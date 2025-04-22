## Overview

PayNowOrLater отображает информацию о возможностях оплаты.

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Desktop = require('./components/View/index.desktop').default;
    const Touch = require('./components/View/index.touch').default;

    const PayNowOrLater = createPlatformProxyComponent({Touch, Desktop});

    let store = createStore(() => {});

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <PayNowOrLater />
        </ViewPort>
    </Provider>
```
