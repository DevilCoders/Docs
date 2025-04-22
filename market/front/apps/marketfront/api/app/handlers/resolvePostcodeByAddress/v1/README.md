# Резолвер resolvePostcodeByAddress

## Описание

Возвращает индекс по переданному адресу и региону

| Parameter | Type   | Description      | Default | Value |
|-----------|--------|------------------| ----- | ----- |
| address*  | string | строка с адресом | - | - |
| regionId  | number | id региона       | - | - |

\* - обязательный параметр

## Пример запроса

```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolvePostcodeByAddress'
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [{
    "address": "Москва, Красная площадь 1",
    "regionId": 213
    }]
}'
```
