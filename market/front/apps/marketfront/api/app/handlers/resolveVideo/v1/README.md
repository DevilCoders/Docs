# Резолвер resolveVideo

## Описание

Возвращает видео из бэкенда `vhFrontend`

## Пример запроса

```bash
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveVideo'
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{
	    "streams": [{uuid: "123", streamId: "234"}, {uuid: "345"}]
    }]
}'
```
