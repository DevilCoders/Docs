# Резолвер removeComparisonItem

Резолвер для удаления элемента из списка сравнения.

Параметры из query запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | Идентификатор установки приложения | - | - |

\* - Обязательный параметр

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `productId`** | number | id продукта | - |
| `sku`** | number | id продукта | - |

\** - Обязательно должен присутствовать один из параметров

## Пример запроса

```
curl --request POST '<FAPI_URL>/api/v1?name=removeComparisonItem&uuid=1' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [{
        "productId": 2,
        "sku": 1,
    }]
}'
```

## Пример ответа резолвера
```json
{
    "results": [
        {
            "handler": "removeComparisonItem",
            "result": "OK"
        }
    ],
    "collections": {}
}
```

Полезные ссылки:

- [Входные параметры](./constraints.js)
