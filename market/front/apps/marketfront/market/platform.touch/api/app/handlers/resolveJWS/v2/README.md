# Резолвер resolveJWS

Резолвер который взвращает jws токен


## QUERY Параметры запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | uuid | - | - |

\* - обязательные параметры

## Параметры тела запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `token`* | string | safetyNet токен | - | - |
| `nonce`* | string | nonce из ручки resolveNonce | - | - |
| `version`* | string | версия приложения | - | - |

\* - обязательные параметры

## Пример запроса резолвера
```bash
curl --location --request POST '<FAPI_HOST>/api/v2?name=resolveJWT&uuid=31fa961c98684e4c8d569b06c99cfc4e' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [
		{
			"token": "1o2",
            "nonce": "8af834612ae428692a6b8e7e6a3e10d4:1600679120",
            "version": "1.0.0"
		}
	]
}'
```

## Пример ответа резолвера

```json
{
    "results": string(jws токен),
    "collections": {}
}
```

## Пример ответа с ошибкой

```json
{
    "results": [
        {
            "handler": "resolveJWS",
            "error": {
                "kind": "ResolveJWSErrorHandler",
                "message": "Nonce '8af834612ae428692a6b8e7e6a3e10d4:1600679120' is not valid"
            }
        }
    ],
    "collections": {}
}
```
