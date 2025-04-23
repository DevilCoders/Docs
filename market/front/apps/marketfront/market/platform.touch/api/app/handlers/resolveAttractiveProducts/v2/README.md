# Резолвер resolveAttractiveProducts

## Описание

Возвращает «привлекательные» (рекомендованные пользователю товары из place=attractive_models) товары. Пользователь должен быть авторизован

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `numdoc` | number | количество товаров | - | - |
| `page` | number | номер страницы ответа | - | - |
| `trim-thumbs` | number | Включает отдачу Репортом обрезанных тумбов без белых полей. | 1 | 0 / 1 |

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v2?name=resolveAttractiveProducts' \
  --header 'content-type: application/json' \
  --data '{
	"params": [{
		"numdoc": 1,
		"page": 0
	}]
}'
```
## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveAttractiveProducts",
      "result": [
        14206682
      ]
    }
  ],
  "collections": {
    "product": Array(),
    "productShowPlace": "Array()",
    "product": "Array()",
    "offerShowPlace": "Array()",
    "offer": "Array()",
    "category": Array(),
    "navnode": Array(),
    "venodr": Array(),
    "shop": Array(),
    "outlet: Array(),
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveProductsByHistory/v2/index.js)
- [Описание сущности `product` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/product/index.js)
