# Резолвер resolveGrowingCashbackStatus

Возвращает статус участия в акции Растущего кешбэка.
Доступен режим мока: нужно передать query-параметр `growing-cashback-mock=default` (или `gotFullReward`)
В режиме мока НЕ пустой ответ будет дан только при передаче реарр флага (`growing_cashback`)

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |

## Пример запроса

```shell script
curl --request POST \
  --url 'https://<FAPI_HOST>/api/v1?name=resolveGrowingCashbackStatus' \
  --header 'Content-Type: application/json' \
  --data '{
	"params": [
      {
      }
    ]
}'
```

## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveGrowingCashbackStatus",
      "result": {
        "id": "growing_cashback_empty",
        "entity": "perkStatus",
        "type": "GROWING_CASHBACK",
        "isPurchased": true,
        "cmsDescriptionSemanticId": null,
        "maxCashbackTotal": 1550,
        "minOrderTotal": {
          "currency": "RUR",
          "value": 3500
        },
        "ordersCount": 3,
        "isGotFullReward": false
      }
    }
  ],
  "collections": {}
}
```
