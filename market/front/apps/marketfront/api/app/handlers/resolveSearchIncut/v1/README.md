# Резолвер resolveSearchIncut

Возвращает коллекцию офферов

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `text`* | string | Поисковый запрос пользователя | - | - |
| `hid`* | number| Идентификатор товарного дерева | - | - |
| `needBanner` | boolean | Отдавать баннер вендора | - | - |
| `filters` | Object | Фильтры | - | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример запроса
```text
curl --location --request POST 'https://madiyetov.api.pokupki.logrus01vd.market.yandex.ru/api/v1?name=resolveSearchIncut' \
--header 'api-platform: android' \
--header 'content-type: application/json' \
--data-raw '{
	"params": [{
		"hid": 13360751
	}]
}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolveSearchIncut",
      "result": {
        "items": "Array(vendorIncutEntity) | Array(offerShowPlace)",
        "incutType": "vendor | shop"
      }
    }
  ],
  "collections": {
    "vendorIncutEntity": "Array()",
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

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveSearchIncut/v1/index.js)
