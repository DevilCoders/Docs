# Резолвер resolveDeliveryConditions

## Описание

Возвращает условия доставки по региону.


| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `regionId`* | integer | ID региона | - | - |
| `shouldCalculateDelivery` | boolean | - | - | - |
| `cpaValue` | 'any' / 'real' | - | - | - |

\* - обязательный параметр

## Пример запроса

```bash
curl --request POST \
  --url 'https://<FAPI_HOST>/api/v1?name=resolveDeliveryConditions' \
  --header 'Content-Type: application/json' \
  --header 'api-platform: IOS' \
  --header 'cache-control: no-cache' \
  --cookie 'is_gdpr=0; is_gdpr_b=CLqUMRD5NQ%3D%3D; i=JiEH4pOVDgC3%2BsAZ3NDzWt8PRJE8zWBRAB6WdLUwrA5ClIWpGbqNhHeFkoWzakyWvuz%2Fyt0Ojsid4kLXjWEI71%2BD1Vs%3D' \
  --data '{
  "params": [
    {
      "regionId": 213
    }
  ]
}'
```
