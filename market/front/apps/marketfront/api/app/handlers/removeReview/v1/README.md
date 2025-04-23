# Резолвер removeReview

## Описание

Резолвер, который позволяет удалить отзыв.
Необходима авторизация.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `reviewId` | number | Айди отзыва | - |

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "removeReview",
            "result": null
        }
    ],
    "collections": {}
}
```

## Пример неуспешного ответа

```
{
    "results": [
        {
            "handler": "removeReview",
            "error": {
                "kind": "ResolverError",
                "message": "Resolver \"removeReview\" failed with error: \"ReviewNotFoundError: Review with id = 60327155 doesn't exist\""
            }
        }
    ],
    "collections": {}
}
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/removeReview/v1/index.js)
