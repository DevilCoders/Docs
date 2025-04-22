# Резолвер resolveSkuInfo

Возвращает информацию о sku из плейса `modelinfo`

Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `skuIds`* | integer[] |  id sku | - | - |
| `productIds` | integer[] |  id product | - | - |
| `billingZone`* | string | pp | - | - |
| `specificationSet`* | string[] | формат отображения характеристик | - | - |
| `showDigitalDsbsGoods` | boolean | Возвращать ли в ответе цифровые дсбс товары  | - | - |
| `fapiParams` | FapiParams | дополнительный параметры передающиеся из мобилок в fapi ручку  | - | - |
| `showPreorder` | boolean | Готовность получать предзаказные оферы (default: false - не готовы)  | - | - |

\* - обязательные параметры

## Пример запроса резолвера
```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveSkuInfo' \
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{
        "skuIds": [100152460142],
        "productIds": [14236972],
        "billingZone": "card",
        "specificationSet": ["msku-friendly"],
        "showDigitalDsbsGoods": true,
        "fapiParams": {
            "cartSnapshot": [{
                "wareMd5": "wareMd5",
                "sku": "123",
            }],
            "gps": "lat41.101010,lon2.101010",
        },
        "showPreorder": true,
    }]
}'```
