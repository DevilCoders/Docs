# Резолвер resolveComparison

## Описание

Резолвер, возвращающий список сравнения (Comparison).

## Параметры из query запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uuid`* | string | Идентификатор установки приложения | - | - |

\* - обязательный параметр

## Параметры тела запроса
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| - | - | - | - | - |

## Пример запроса
```
curl --request POST '<FAPI_URL>/api/v1?name=resolveComparison&uuid=1a' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{}]
}'
```

## Пример ответа
```
{
    "results": [
        {
            "handler": "resolveComparison",
            "result": [
                "91491"
            ]
        }
    ],
    "collections": {
        "userComparisonList": [
            {
                "categoryId": "91491",
                "lastUpdate": 1596112003000,
                "items": [
                    {
                        "productId": "3",
                        "sku": 3,
                        "lastUpdate": 1596112003000
                    },
                    {
                        "productId": "2",
                        "sku": 4,
                        "lastUpdate": 1596040078000
                    }
                ]
            }
        ],
        "category": [
            {
                "id": 91491,
                "fullName": "Мобильные телефоны"
            }
        ]
    }
}
```

## Полезные ссылки

[Тип UserComparisonList](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/userComparisonList/index.js#L15)<br>
[Тип Category](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/category/index.js#L10)*

\* - из типа category используется только поля  `id` и `fullName`
