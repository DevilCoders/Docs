# Резолвер addItemToComparison

## Описание

Резолвер, добавляющий продукты в список сравнения (Comparison)

Параметры из query запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | Идентификатор установки приложения | - | - |
\* - обязательный параметр


Параметры из тела запроса:

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `items`* | array | Массив элементов для добавления в список | - | - |
| `items.categoryId`* | string | id категории, он же hid | - | - |
| `items.productId`** | number | id товара | - | - |
| `items.sku`** | number | sku товара | - | - |

\* — обязательный параметр<br>
\** - минимум один из этих элементов

Пример запроса:
```
curl --request POST '<FAPI_HOST>/api/v1?name=addItemToComparison' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [{
        "items": [
            {
                "productId": 14206636,
                "categoryId": "91491",
                "sku": 1
            }
        ]
    }]
}'
```

Возвращает пустой ответ
```
{
  "results": [
    {
      "handler": "addItemToComparison",
      "result": 'OK'
    }
  ],
  "collections": {}
}
```

Полезные ссылки:

- [Входные параметры](./constraints.js)
