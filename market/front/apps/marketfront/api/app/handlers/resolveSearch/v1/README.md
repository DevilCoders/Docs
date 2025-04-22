## Резолвер resolveSearch

Возвращает выдачу репорта из метода `prime`.
**Умеет в редиректы** на каталог.
Данные в ответе резолвера нормализованы.


## Параметры из тела запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `text`* | string | Поисковый запрос пользователя | - | - |
| `page`** | number |  Номер страницы | 1 | - |
| `hid`* | number| Идентификатор товарного дерева | - | - |
| `nid` | number| Идентификатор навигационного дерева | - | - |
| `cvredirect` | number| Нужен ли редирект | 0 | 1 |
| `billingZone` | string | Место показа. [Список ключей](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/report/constants.js#L122-L154) | - |
| `fapiParams` | object | функционал priceDrop [тип](https://github.yandex-team.ru/market/marketfront/blob/master/src/resolvers/report/resolveCommonReportParams.js#L19) | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример запроса


```text
curl --location --request POST '<FAPI_URL>/api/v1?name=resolveSearch' \
--header 'api-platform: android' \
--header 'content-type: application/json' \
--data-raw '{
	"params": [{
		"page": 1,
		"text": "iphone x",
		"billingZone": "default",
		"blenderPattern": "0x1e07"
	}]
}'
```


## Пример ответа

```json
{
  "results": [
    {
      "handler": "resolveSearch",
      "result": "oe222y80v8"
    }
  ],
  "collections": {
    "visibleSearchResult": [
      {
        "id": "oe222y80v8",
        "text": [
            "iphone x"
        ],
        "page": 1,
        "searchResultIds": {
          "1": "mz1yqncc1p"
        },
        "sortId": "aprice",
        "sortIds": "Array()",
        "filterIds": "Array()",
        "intentIds": "Array()"
      }
    ],
    "searchResult": [
      {
        "id": "mz1yqncc1p",
        "visibleEntityIds": [
          "productShowPlace_1759344092_15802173990375625061216001",
          "productShowPlace_217317885_15802173990375625061216002",
          "productShowPlace_92352002_15802173990375625061216003",
          "productShowPlace_71309158_15802173990375625061216004",
          "productShowPlace_217312163_15802173990375625061216005",
          "productShowPlace_217312269_15802173990375625061216006",
          "productShowPlace_14206636_15802173990375625061216007",
          "productShowPlace_217312280_15802173990375625061216008",
          "productShowPlace_217311018_15802173990375625061216009",
          "productShowPlace_217320262_15802173990375625061216010"
        ]
      }
    ],
    "visibleEntity": "Array()",
    "productShowPlace": "Array()",
    "product": "Array()",
    "offerShowPlace": "Array()",
    "offer": "Array()"
  }
}
```

## Полезные ссылки
[Все параметры репорта](https://wiki.yandex-team.ru/Market/Verstka/report-query-params/)
[Price drop](https://wiki.yandex-team.ru/users/realtim/PriceDrop/LimitedEdition/)
