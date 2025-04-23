# Резолвер resolveOrdersCashbackDetails

## Описание

Возвращает детализацию кешбэка по заказам.

| Parameter    | Type     | Description              | Default    | Value |
| ------------ |----------| ------------------------ | ---------- | ----- |
| `orderIds`\* | number[] | список id заказов        | -          | -     |
| `type`       | enum     | Тип возвращаемого ответа | "separate" | -     |

\* - обязательный параметр

Параметр `type` имеет след значения:

-   `separate` - детализация возвращается отдельно для каждого заказа в поле "orders"
-   `merged` - детализация для всех заказов сразу, в поле "merged"
-   `full` - детализация как отдельно по заказам так и вместе, приходят оба поля

## Пример запроса

```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1/?name=resolveOrdersCashbackDetails' \
--header 'api-platform: ANDROID' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [
        {
            "orderIds": [3301],
            "type": "full"
        }
    ]
}'
```
