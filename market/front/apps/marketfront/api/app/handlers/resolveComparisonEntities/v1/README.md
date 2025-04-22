
# Резолвер resolveComparisonEntities

## Описание

Возвращает модели и sku с полными характеристиками для сравнения

**Важно**
Репорт не возвращает `opinionCount` и `rating` для sku, но в sku
есть `productId` модели, по которому ее можно достать из коллекций и получить нужные поля.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productIds`* | number[] | массив id моделей | - | - |
| `skuIds`* | number[] | массив id sku | - | - |
| `billingZone` | string | массив id sku | default | - |

\* - Должен присутствовать хотя бы один из

## Пример запроса
```
curl --request POST '<FAPI_URL>/api/v1?name=resolveComparisonEntities' \
--header 'Content-Type: application/json' \
--data '{
    "params": [{
        "productIds": [14206636],
        "skuIds": [100131945014]
    }]
}'
```

## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveComparisonEntities",
        "result": {
          "product": ["1"],
          "sku": [1]
        }
    }
  ],
  "collections": type SkuCollectionsWithProduct
}
```

## Полезные ссылки
- [Описание сущности Product](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/product/index.js#L32)
- [Описание сущности Sku](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/sku/index.js#L31)
- [Описание сущности Specs](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/specs/index.js)
