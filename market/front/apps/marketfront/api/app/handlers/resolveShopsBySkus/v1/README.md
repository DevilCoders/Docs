# Резолвер resolveShopsBySkus

## Описание

Возвращает список магазинов, содержащих полный или частичный список товаров, переданных в параметры

## Параметры
| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `regionId`* | integer | ID региона | - | - |
| `items`* | array | Массив данных товаров (marketSku, count) | - | - |
| `geo` | object | Данные карты (zoom, mapBound) | - | - |
| `maxOutlets` | integer | Максимальное количество возвращаемых аутлетов | - | - |

\* - обязательный параметр

## Пример запроса

```bash
curl --location --request POST '<FAPI_HOST>/api/v1/?name=resolveShopsBySkus' \
--header 'Content-Type: application/json' \
--header 'api-platform: ANDROID' \
--header 'X-App-Version: 3.31' \
--header 'X-Region-Id: 213' \
--data-raw '{
    "params": [
        {
            "regionId": 213,
            "items": [
                {
                    "marketSku":"101302298764",
                    "count": 1
                },
                {
                    "marketSku":"101348308734",
                    "count": 1
                },
                {
                    "marketSku":"664895281",
                    "count": 1
                }
            ]
        }
    ]
}'
```
