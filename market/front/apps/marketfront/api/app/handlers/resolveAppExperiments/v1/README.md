# Резолвер resolveAppExperiments


## Пример запроса

```bash
curl --insecure --location --request POST '<FAPI_URL>/api/v1?name=resolveAppExperiments' \
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'User-Agent: Beru/370 (iPhone; iOS 14.5; Scale/2.00)' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{
        "forcedExperiments": ["367974", "363731", "345205"],
        "supportedExperiments": [""]
    }]
}'
```
