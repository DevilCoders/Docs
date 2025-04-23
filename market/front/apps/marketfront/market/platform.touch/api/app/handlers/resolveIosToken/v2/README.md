# Резолвер resolveIosToken

Резолвер который взвращает ios токен


## QUERY Параметры запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | uuid | - | - |

\* - обязательные параметры

## Параметры тела запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `token`* | string | safetyNet токен | - | - |
| `version`* | string | версия приложения | - | - |

\* - обязательные параметры

## Хэдеры состояния проверки токена

```json
{
	headers: {
		"x-jws-status": "empty" / "invalid"
	}
}
```

## Пример запроса резолвера
```bash
curl --location --request POST '<FAPI_HOST>/api/v2?name=resolveIosToken&uuid=31fa961c98684e4c8d569b06c99cfc4e' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [
		{
			"token": "1o2",
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
            "handler": "resolveIosToken",
            "error": {
                "kind": "ResolveIosErrorHandler",
                "message": "Invalid DeviceCheck token"
            }
        }
    ],
    "collections": {}
}
```