# Резолвер resolveProductFactorsByCategoryV2

## Описание

Выдаёт набор факторов по заданной категории товаров.
Факторы используются для сохранения пользователем во время создания отзывов.


## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `categoryId` | number | Айди категории | - |

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "resolveProductFactorsByCategory",
            "result": [
                2927,
                1059,
                1060,
                1061,
                1062
            ]
        }
    ],
    "collections": {
        "productFactor": [
            {
                "id": 1059,
                "title": "Общее впечатление",
                "order": 10,
                "priority": false,
                "description": null,
                "type": 0,
                "radioValues": null
            },
            {
                "id": 1060,
                "title": "Соответствие заявленному размеру",
                "order": 20,
                "priority": false,
                "description": null,
                "type": 0,
                "radioValues": null
            },
            {
                "id": 1061,
                "title": "Качество материалов",
                "order": 30,
                "priority": false,
                "description": null,
                "type": 0,
                "radioValues": null
            },
            {
                "id": 1062,
                "title": "Качество пошива",
                "order": 40,
                "priority": false,
                "description": null,
                "type": 0,
                "radioValues": null
            },
            {
                "id": 2927,
                "title": "Вещь соответствует заявленному размеру?",
                "order": 0,
                "priority": true,
                "description": null,
                "type": 1,
                "radioValues": [
                    {
                        "value": 0,
                        "order": 0,
                        "name": "Да"
                    },
                    {
                        "value": 1,
                        "order": 10,
                        "name": "Нет, маломерит"
                    },
                    {
                        "value": 2,
                        "order": 20,
                        "name": "Нет, большемерит"
                    }
                ]
            }
        ]
    }
}
```

## Пример неуспешного ответа

```
{
  "results": [
    {
      "handler": "resolveProductFactorsByCategory",
      "error": {
        "kind": "ValidationParamsHandlerError",
        "message": "Param \"categoryId\" is not an integer or integer like string (qwe)"
      }
    }
  ],
  "collections": {}
}
```
