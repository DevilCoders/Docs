# Резолвер removeComparisonCategory

Резолвер для удаления элемента из списка сравнения.

Параметры из query запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid` | string | Идентификатор установки приложения | - | - |

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `categoryId`* | string | id продукта | - |

\* - Обязательный параметр

## Пример запроса

```
curl --request POST '<FAPI_URL>/api/v1?name=removeComparisonCategory&uuid=1' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [{
        "categoryId": "1",
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
