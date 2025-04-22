# Резолвер resolveCompetitiveCard

Возвращает коллекцию моделей

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `hyperid`* | number | Id модели | - | - |

\** - обязательный параметр

## Пример запроса
```text
curl --location --request POST '<FAPI_URL>/api/v1?name=resolveCompetitiveCard' \
--header 'api-platform: android' \
--header 'content-type: application/json' \
--data-raw '{
	"params": [{
		"hyperid": 598754052
	}]
}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolveCompetitiveCard",
      "result": "Array(productShowPlace)"
    }
  ],
  "collections": {
    "productShowPlace": "Array()",
    "offerShowPlace": "Array()",
    "offer": "Array()",
    "shop": "Array()",
    "navnode": "Array()",
    "category": "Array()",
    "vendor": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveCompetitiveCard/v1/index.js)
