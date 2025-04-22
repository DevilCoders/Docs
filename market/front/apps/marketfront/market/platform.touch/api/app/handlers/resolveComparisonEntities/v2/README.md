# Резолвер resolveComparisonEntities

Резолвер для списка моделей сравнения и их характеристики.
Данные в ответе резолвера нормализованы.

Если передать массив с id моделей, то веренется список сравнения состоящий из переданных id. Если
Массив не переделан то вернется список сравнения текущего пользователя по переданной категории.


## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `hid`* | number | id категории | - |
| `productIds` | number[] | массив id моделей | - |

\* - обязательный параметр

## Пример ответа резолвера
```
{
    "results": [
        {
            "handler": "resolveComparisonEntities",
            "result": string[] // массив id моделей
        }
    ],
    "collections": {
        "product": type ProductMinCollections[],
        "spec": type ProductComparisonCollection[]
    }
}
```

- [Тип модели](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/product/index.js#L34)
- [Тип характеристик](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/productComparison/index.js#L35)
