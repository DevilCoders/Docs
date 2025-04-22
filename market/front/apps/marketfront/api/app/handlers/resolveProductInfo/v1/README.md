# Резолвер resolveProductInfo

Возвращает информацию о меодели из плейса `modelinfo`

Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productIds`* | integer[] |  id моделей | - | - |
| `billingZone`* | string | pp | - | - |
| `specificationSet`* | string | формат отображения характеристик | -| - |
| `showDigitalDsbsGoods` | boolean | Возвращать ли в ответе цифровые дсбс товары  | -| - |

\* - обязательные параметры

## Пример запроса резолвера
```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveProductInfo' \
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [{
        "productIds": [1759344315],
        "billingZone": "card",
        "specificationSet": ["full"],
        "cpa": "real",
        "rgb": "green"
    }]
}'
```
