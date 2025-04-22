# Резолвер callClickDaemon

Дёргает кликдемон

## Параметры

| Parameter | Type          | Description   | Default | Value |
|-----------|---------------|---------------|---------| ----- |
| `urls`**  | Array(string) | Ссылки демона | - | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример запроса
```text
curl --location --request POST 'https://<FAPI_URL>/api/v1?name=callClickDaemon' \
--header 'api-platform: android' \
--header 'content-type: application/json' \
--data-raw '{
	"params": [{
		"urls": ["link1", "link2"]
	}]
}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "callClickDaemon",
      "result": "true"
    }
  ],
  "collections": {}
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/callClickDaemon/v1/index.js)
