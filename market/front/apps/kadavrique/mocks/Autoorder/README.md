# AutoorderApi

Данные в стейте:

```
{
    requests: [
        {
            id: '1',
            supplierId: 1000569488,
            responseDeadline: '2021-05-01',
            deliveryDeadline: '2021-05-15',
            created: '2021-04-15T15:30:47',
            status: SUPPLY_REQUEST_STATUS.SUPPLIER_ACCEPTED,
            warehouse: {
                id: 145,
                name: 'Маршрут',
                code: null,
                type: 'FULFILLMENT',
                region: {
                    id: 145,
                    name: 'MSK',
                    fallbackRegionId: null,
                }
            }
        }
    ],
    ffShopRequests: [
        {
            supplierRequestId: 'requestId',
            ffShopRequestsIds: [1, 2, 3],
        },

    ],
}
```

## getFFShopRequests

Возвращает массив связей заявок на поставку к поставке

```
[
    {
        supplierRequestId: '1',
        ffShopRequestsIds: [1, 2, 3],
    }
]
```

## getSupplierRequests

Возвращает массив заявок на поставку + их количество, можно фильтровать по параметру status (строка или массив строк)

Параметры:
```
{
    params: {
        status: 'NEW'
    }
}

{
    params: {
        status: ['NEW', 'OUTDATED']
    }
}
```

Возвращает:
```
{
    requests: [
        {
            id: '1',
            supplierId: 1000569488,
            responseDeadline: '2021-05-01',
            deliveryDeadline: '2021-05-15',
            created: '2021-04-15T15:30:47',
            status: SUPPLY_REQUEST_STATUS.SUPPLIER_ACCEPTED,
            warehouse: {
                id: 145,
                name: 'Маршрут',
                code: null,
                type: 'FULFILLMENT',
                region: {
                    id: 145,
                    name: 'MSK',
                    fallbackRegionId: null,
                }
            }
        }
    ],
    count: 1
}
```
## saveSupplierRequest

Принимает или отклоняет запрос на поставку

Параметры:
```
{
    params: {
        id: '1'
    },
    body: {
        accept: true
    }
}
```
