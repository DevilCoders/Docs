# Резолвер resolveDeliveryBuckets

## Описание

Возвращает лучший магазин доставлюющих товары из списка.


| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `regionId`* | integer | ID региона | - | - |
| `items`* | array | Массив данных товаров (marketSku, count, wareId) | - | - |
| `expressDelivery` | boolean | экспресс доставка | - | - |
| `preferableCourierDeliveryDay` | integer | доставка "сегодня" или "завтра" | - | - |

\* - обязательный параметр

## Пример запроса

```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveDeliveryBuckets'
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [
	  {
	    "regionId": 213,
	    "items": [
	      {
	        wareId: '7yTm-nWSQL5wPnSGN0-AnQ',
	        marketSku: '228007832',
	        count: 1,
	      },
	    ],
	    "preferableCourierDeliveryDay": 0,
	  }
	]
}'
```
