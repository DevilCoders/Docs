Виджет документов по заказу

- Синглтон, всегда 1 на странице
- Необходим OrderCollections в коллекциях страницы (пока нет кэширющего резолвера для заказов)
- Показывается/скрывается по внешним @self/root/src/actions/orderDocuments
- Для десктопа - открывает popup со списком ссылок на чеки, каждая ссылка открывает pdf чека.
- Для тача - рисует отдельный экран

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('./components/View/index.touch').default;
    const Desktop = require('./components/View/index.desktop').default;
    const OrderDocumentsComponent = createPlatformProxyComponent({Touch, Desktop});

    const orderProps = {
        orderId: 1,
        orderReceiptIds: [11, 22],
        isLoading: false,
        isLoadingFinished: true,
        hasError: false,
        isWarrantyShown: false,
        fetchOrderReceipts: () => {},
    };

    let store = createStore(() => ({
        widgets: {
            OrderDocuments: {
                // данные, которые потом будут в State.widget
                [1]: {
                    orderId: 1,
                    orderReceiptIds: [11, 22],
                    isShown: true,
                    isLoading: false,
                    isLoadingFinished: true,
                    isWarrantyShown: false,
                    hasError: false,
                },
            },
        },
        collections: {
            order: {
                1: {
                    id: 1,
                    status: 'DELIVERED',
                }
            },
            orderReceipt: {
                11: {
                    id: 11,
                    type: 'INCOME',
                    createdAt: 1478165459000,
                },
                22: {
                    id: 22,
                    type: 'INCOME_RETURN',
                    createdAt: 1478168459000,
                },
            },
        },
    }));

    <Provider store={store}>
        <ViewPort width={1000} height={600}>
            <OrderDocumentsComponent {...orderProps} />
        </ViewPort>
    </Provider>
```
