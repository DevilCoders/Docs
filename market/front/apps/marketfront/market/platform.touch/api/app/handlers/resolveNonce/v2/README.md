
# Резолвер resolveNonce

Резолвер который генерирует одноразовый код, для запроса JWT

## QUERY Параметры запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | uuid | - | - |

\* - обязательные параметры


## Пример запроса резолвера
```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v2?name=resolveNonce&uuid=1a' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [
		{}
	]
}'
```

## Пример ответа резолвера

```json
{
    "results": string (nonce),
    "collections": {}
}
```

