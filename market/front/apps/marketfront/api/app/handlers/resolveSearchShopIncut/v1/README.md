# Резолвер resolveSearchShopIncut

Возвращает коллекцию офферов

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `text`* | string | Поисковый запрос пользователя | - | - |
| `hid`* | number| Идентификатор товарного дерева | - | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример запроса
```text
curl --location --request POST '<FAPI_URL>/api/v1?name=resolveSearchShopIncut' \
--header 'api-platform: android' \
--header 'content-type: application/json' \
--data-raw '{
	"params": [{
		"hid": 14994593
	}]
}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolveSearchShopIncut",
      "result": [
        "ohtoEbFZus06tFaDVhGSDLOtRIVsK1lR1CiNWzVaBj6dTLcfmiEeUUEtD5H6OpKXBdB39ckAD_yb_jMrVytEvPcBez3AcsBlLuBQ3USBoGasIy2agHLxVsPEwFuqhyQuAQywHcMXoNs,",
        "cl0e5M2t_JCGRlPFNk1o2iXtMK6wWSCL16v62muR-fOgHc545C5ko5x9STSRoCg92axY8-Huhvd-Xv8OobBvyaY3FfJzHHWmFsI9sbeslVc0uxFx1_iixxEdwL16svoX89JI77hiPrQ,"
      ]
    }
  ],
  "collections": {
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

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveSearchShopIncut/v1/index.js)
