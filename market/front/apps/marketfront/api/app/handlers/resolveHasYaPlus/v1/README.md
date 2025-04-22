# Резолвер resolveHasYaPlus

## Описание

TODO


| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| TODO | TODO | TODO | - | - |

\* - обязательный параметр

## Пример запроса

```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveSearch'
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{
		"page": 2,
        "adult": 1,
		"numdoc": 2,
		"text": "красный",
        "billingZone": "default",
		"fapiParams": {
			"cartSnapshot": []
		},
        "non-dummy-redirects": 1,
        "rgb": "blue",
        "cpa": "real",
        "allowCollapsing": 1
    }]
}'
```
