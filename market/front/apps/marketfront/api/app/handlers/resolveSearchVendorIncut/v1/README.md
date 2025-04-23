# Резолвер resolveSearchVendorIncut

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
curl --location --request POST 'https://madiyetov.api.pokupki.logrus01vd.market.yandex.ru/api/v1?name=resolveSearchVendorIncut' \
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
      "handler": "resolveSearchVendorIncut",
      "result": [
        "vendorIncutEntity_vendorBanner_42",
        "vendorIncutEntity_productShowPlace_771371012_16196895610027004561216001",
      ]
    }
  ],
  "collections": {
    "vendorIncutEntity": [
      {
        "id": "vendorIncutEntity_vendorBanner_42",
        "entity": "vendorIncutEntity",
        "referenceEntity": "vendorBanner",
        "vendorBannerId": "42"
      },
      {
        "id": "vendorIncutEntity_productShowPlace_771371012_16196895610027004561216001",
        "entity": "vendorIncutEntity",
        "referenceEntity": "productShowPlace",
        "productShowPlaceId": "16196895610027004561216001"
      }
    ],
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

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveSearchVendorIncut/v1/index.js)
