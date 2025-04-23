# Резолвер resolveProductFactorsByCategory

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
        801,
        802,
        803,
        804,
        805
      ]
    }
  ],
  "collections": {
    "productFactor": [
      {
        "id": 801,
        "title": "Звук",
        "order": null,
        "description": null
      },
      {
        "id": 802,
        "title": "Удобство ношения",
        "order": null,
        "description": null
      },
      {
        "id": 803,
        "title": "Надежность",
        "order": null,
        "description": null
      },
      {
        "id": 804,
        "title": "Качество сборки",
        "order": null,
        "description": null
      },
      {
        "id": 805,
        "title": "Звукоизоляция",
        "order": null,
        "description": null
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
Ссылочки:

- [Входные параметры](./constraints.js)
- [Описание формата](https://raw.github.yandex-team.ru/market/microformats/master/productFactor/productFactor.json)
- [Описание сущности в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/productFactor/index.js)
