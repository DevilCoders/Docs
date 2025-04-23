# Резолвер resolveComparison

Резолвер, возвращает списки сравнения.
Данные в ответе резолвера нормализованы.


## Пример ответа резолвера
```
{
    "results": [
        {
            "handler": "resolveComparison",
            "result": string[]
        }
    ],
    "collections": {
        "userComparisonList": [
            {
                "categoryId": string,
                "lastUpdate": number,
                "items": [
                    {
                        "productId": string,
                        "lastUpdate": number
                    }
                ]
            }
        ],
        "category": [
            {
                "id": number,
                "fullName": string
            }
        ]
    }
}
